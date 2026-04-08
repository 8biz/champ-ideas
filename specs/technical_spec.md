# Technische Spezifikation

**Projekt**: champ – Ringkampfsport-Wettbewerbs-Management-Tool  
**Version**: 0.1.0 (Entwurf)  
**Stand**: 2026-04-08  

---

## 1. Systemarchitektur

Das Tool wird als **Web-Applikation** mit einer klassischen **3-Schichten-Architektur** umgesetzt:

```
┌────────────────────────────────────────────┐
│              Frontend (Browser)            │
│         React.js / TypeScript / PWA        │
└────────────────┬───────────────────────────┘
                 │ HTTP/REST + WebSocket
┌────────────────▼───────────────────────────┐
│            Backend (API-Server)            │
│     Node.js + Express / NestJS             │
└────────────────┬───────────────────────────┘
                 │ SQL / ORM
┌────────────────▼───────────────────────────┐
│                Datenbank                   │
│     PostgreSQL (Produktion) / SQLite       │
└────────────────────────────────────────────┘
```

### 1.1 Überblick Komponenten

| Komponente       | Technologie                         | Beschreibung                                  |
|------------------|-------------------------------------|-----------------------------------------------|
| Frontend         | React.js 18+, TypeScript, Vite      | Single Page Application (SPA) / PWA           |
| UI-Bibliothek    | Tailwind CSS + shadcn/ui            | Responsives Design, Komponenten-Bibliothek    |
| Backend API      | Node.js 20+, NestJS, TypeScript     | RESTful API + WebSocket-Server                |
| ORM              | Prisma                              | Datenbankzugriff und Migrations               |
| Datenbank        | PostgreSQL 15+                      | Hauptdatenbank für Produktion                 |
| Cache/Sessions   | Redis                               | Session-Management, Echtzeit-Pub/Sub          |
| Authentifizierung| JWT + Passport.js                   | Token-basierte Authentifizierung              |
| WebSockets       | Socket.io                           | Echtzeit-Kommunikation für Live-Anzeige       |
| Datei-Export     | PDFKit / ExcelJS                    | PDF- und Excel-Generierung                    |
| Testing          | Jest + Supertest + Playwright       | Unit-, Integration- und E2E-Tests             |
| CI/CD            | GitHub Actions                      | Automatisierte Tests und Deployments          |
| Containerisierung| Docker + Docker Compose             | Lokale Entwicklung und Deployment             |
| Hosting          | Hetzner Cloud / AWS                 | Produktions-Infrastruktur                     |

---

## 2. Datenbankschema (Entwurf)

### Zentrale Entitäten

```sql
-- Turniere
Tournament (id, name, date, location, organizer, discipline, status, created_at)

-- Gewichtsklassen
WeightClass (id, tournament_id, name, min_weight, max_weight, age_group)

-- Athleten
Athlete (id, first_name, last_name, birthdate, gender, club, license_number,
         weight_class_id, tournament_id, actual_weight, status)

-- Kämpfe
Match (id, tournament_id, weight_class_id, round, mat_number,
       athlete_red_id, athlete_blue_id, scheduled_time, status,
       winner_id, result_type, duration_seconds)

-- Kampfergebnisse / Punkte-Log
MatchEvent (id, match_id, timestamp, event_type, athlete_id, points, note)

-- Benutzer / Rollen
User (id, username, email, password_hash, role, tournament_id)

-- Vereine
Club (id, name, short_name, federation_id, contact_email)
```

---

## 3. API-Endpunkte (Auswahl)

### Tourniere
| Methode | Pfad                        | Beschreibung                         |
|---------|-----------------------------|--------------------------------------|
| GET     | `/api/tournaments`          | Alle Turniere auflisten              |
| POST    | `/api/tournaments`          | Neues Turnier erstellen              |
| GET     | `/api/tournaments/:id`      | Turnierdetails abrufen               |
| PATCH   | `/api/tournaments/:id`      | Turnier aktualisieren                |

### Athleten
| Methode | Pfad                           | Beschreibung                      |
|---------|--------------------------------|-----------------------------------|
| GET     | `/api/tournaments/:id/athletes`| Athleten eines Turniers           |
| POST    | `/api/athletes`                | Athleten registrieren             |
| PATCH   | `/api/athletes/:id`            | Athletendaten aktualisieren       |
| POST    | `/api/athletes/import`         | CSV/Excel Import                  |

### Kämpfe
| Methode | Pfad                           | Beschreibung                      |
|---------|--------------------------------|-----------------------------------|
| GET     | `/api/tournaments/:id/matches` | Kampfplan abrufen                 |
| POST    | `/api/matches/generate`        | Paarungen automatisch erzeugen    |
| PATCH   | `/api/matches/:id/start`       | Kampf starten                     |
| PATCH   | `/api/matches/:id/end`         | Kampf beenden                     |
| POST    | `/api/matches/:id/events`      | Kampfereignis (Punkte) speichern  |

### WebSocket-Events
| Event               | Richtung         | Beschreibung                         |
|---------------------|------------------|--------------------------------------|
| `match:started`     | Server → Client  | Kampf wurde gestartet                |
| `match:score`       | Server → Client  | Punktestand-Aktualisierung           |
| `match:ended`       | Server → Client  | Kampf beendet, Ergebnis bekannt      |
| `bracket:updated`   | Server → Client  | Turnierbaum aktualisiert             |

---

## 4. Frontend-Architektur

### Seitenstruktur

```
/                        → Öffentliche Startseite / Turnierinformationen
/live                    → Live-Anzeige (öffentlich)
/live/mat/:id            → Scoreboard-Modus für eine Matte
/admin                   → Admin-Dashboard (geschützt)
/admin/tournaments       → Turnierverwaltung
/admin/athletes          → Teilnehmerverwaltung
/admin/matches           → Kampfplan
/admin/results           → Ergebnisauswertung
/referee/:matchId        → Schiedsrichter-Interface (Tablet-optimiert)
/login                   → Anmeldeseite
```

### State-Management
- Globaler Zustand via **Zustand** (leichtgewichtig) oder **Redux Toolkit** (bei hoher Komplexität)
- Server-State via **TanStack Query** (React Query)
- WebSocket-Verbindung als persistenter Service

---

## 5. Sicherheitskonzept

- **Authentifizierung**: JWT-Token (Access-Token: 15 Min, Refresh-Token: 7 Tage)
- **Autorisierung**: Role-Based Access Control (RBAC) auf API-Ebene
- **Datenverschlüsselung**: TLS 1.3 für alle Verbindungen
- **Passwort-Hashing**: Argon2id
- **Input-Validierung**: Strict schema validation mit Zod (Frontend + Backend)
- **Rate-Limiting**: API-Anfragen auf 100 Requests/Minute pro IP begrenzt
- **CORS**: Nur explizit erlaubte Origins
- **DSGVO**: Personenbezogene Daten minimieren, Löschfunktion implementieren

---

## 6. Deployment

### Lokale Entwicklung

```bash
# Voraussetzungen: Docker, Node.js 20+, pnpm
git clone https://github.com/8biz/champ-ideas.git
cd champ-ideas
docker compose up -d          # PostgreSQL + Redis starten
pnpm install                  # Abhängigkeiten installieren
pnpm run db:migrate           # Datenbankmigrationen
pnpm run dev                  # Frontend + Backend starten
```

### Produktions-Deployment
- Docker-Images werden via GitHub Actions gebaut und in GitHub Container Registry (ghcr.io) gepusht.
- Deployment auf einem Hetzner VPS via Docker Compose oder Kubernetes (k3s).
- Nginx als Reverse Proxy mit automatischem TLS via Let's Encrypt (Certbot).

### Umgebungsvariablen (Beispiel)
```
DATABASE_URL=postgresql://user:pass@localhost:5432/champ
REDIS_URL=redis://localhost:6379
JWT_SECRET=<secure-random-string>
PORT=3000
FRONTEND_URL=https://champ.example.com
```

---

## 7. Testkonzept

| Testart        | Tool              | Ziel                                          |
|----------------|-------------------|-----------------------------------------------|
| Unit-Tests     | Jest              | Einzelne Funktionen und Services              |
| Integrations-  | Jest + Supertest  | API-Endpunkte mit Test-Datenbank              |
| E2E-Tests      | Playwright        | Komplette User-Flows im Browser               |
| Lasttest       | k6                | Performance unter Turnier-Bedingungen          |

**Ziel**: Mindestens 80 % Testabdeckung für Business-Logik.

---

## 8. Technische Schulden & Risiken

| Risiko                                   | Wahrscheinlichkeit | Maßnahme                                         |
|------------------------------------------|--------------------|--------------------------------------------------|
| Schlechtes WLAN in Sporthallen           | Hoch               | Offline-Modus / lokale Datenhaltung              |
| Gleichzeitige Bearbeitung durch mehrere  | Mittel             | Optimistic Locking / Konfliktauflösung           |
| Datenverlust bei Absturz                 | Niedrig            | Regelmäßige Backups, Transaktionen               |
| Skalierbarkeit bei großen Turnieren      | Niedrig            | Horizontale Skalierung via Docker/k8s            |
