# Anforderungen

Diese Datei enthält die technischen und funktionalen Anforderungen an das Ringkampfsport-Wettbewerbs-Management-Tool.

## 1. Zielgruppe

- **Primär**: Wettkampfleiter, Kampfrichter und Kampfgericht bei Ringkampfsport-Veranstaltungen
- **Sekundär**: Athleten, Trainer und Vereinsvertreter (für Registrierung und Ergebnisverfolgung)
- **Tertiär**: Zuschauer und Öffentlichkeit (für Live-Anzeige und Ergebnisse)

---

## 2. Funktionale Anforderungen

### 2.1 Muss-Kriterien (Must-Have)
| ID   | Anforderung                                                                 |
|------|-----------------------------------------------------------------------------|
| F-01 | Athleten registrieren und verwalten                                          |
| F-02 | Automatische Einteilung in Gewichtsklassen und Altersgruppen                 |
| F-03 | Kampfpaarungen automatisch erstellen (KO, Doppel-KO, Round-Robin)            |
| F-04 | Kampfergebnisse in Echtzeit erfassen und speichern                           |
| F-05 | Live-Anzeige der aktuellen Kämpfe und Ergebnisse                             |
| F-06 | Turnierbracket visuell darstellen                                            |
| F-07 | Endgültige Rangliste und Ergebnisliste exportieren (PDF)                     |
| F-08 | Mehrere Benutzerrollen mit unterschiedlichen Zugriffsrechten                 |

### 2.2 Soll-Kriterien (Should-Have)
| ID   | Anforderung                                                                 |
|------|-----------------------------------------------------------------------------|
| S-01 | Import von Teilnehmerlisten aus CSV/Excel                                    |
| S-02 | Benachrichtigungen bei Kampfaufruf (App-Notification oder Bildschirmanzeige) |
| S-03 | Vereinswertung und Teamrangliste berechnen                                   |
| S-04 | Statistiken und Auswertungen anzeigen                                        |
| S-05 | Mehrsprachige Benutzeroberfläche (Deutsch, Englisch)                         |
| S-06 | Urkunden und Startlisten drucken                                             |

### 2.3 Kann-Kriterien (Could-Have)
| ID   | Anforderung                                                                 |
|------|-----------------------------------------------------------------------------|
| C-01 | Mobilgeräte-App für Athleten (Kampfaufruf, Ergebnisse)                       |
| C-02 | Integration mit nationalen Verbandsdatenbanken                               |
| C-03 | Offline-Modus mit automatischer Synchronisation                              |
| C-04 | SMS-Benachrichtigungen                                                       |
| C-05 | Video-Integration (Kamerasystem für Schiedsrichterunterstützung)             |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Performance
- Die Anwendung muss bis zu **500 gleichzeitige Nutzer** unterstützen.
- Kampfergebnisse müssen innerhalb von **1 Sekunde** in der Live-Anzeige erscheinen.
- Seitenaufbau und Datenbankabfragen müssen unter **2 Sekunden** bleiben.

### 3.2 Verfügbarkeit
- Die Anwendung muss an einem Turniertag eine **Verfügbarkeit von 99,9 %** gewährleisten.
- Datensicherung erfolgt automatisch alle **15 Minuten** auf einen Backup-Server.

### 3.3 Sicherheit
- Zugang nur für autorisierte Benutzer (Authentifizierung erforderlich).
- Datenschutz gemäß **DSGVO** (nur notwendige personenbezogene Daten erheben).
- Passwörter werden gehasht und gesalzen gespeichert (bcrypt oder Argon2).
- Alle Verbindungen über **HTTPS/TLS**.

### 3.4 Benutzerfreundlichkeit
- Intuitive Bedienung ohne lange Einarbeitung (max. 1 Stunde Schulung).
- Responsive Design für Tablets und Desktop-PCs.
- Barrierefreiheit gemäß WCAG 2.1 Level AA.

### 3.5 Wartbarkeit
- Code dokumentiert nach einheitlichem Standard.
- Automatisierte Tests mit einer Abdeckung von mindestens **80 %**.
- Modulare Architektur für einfache Erweiterbarkeit.

---

## 4. Technische Anforderungen

### 4.1 Plattform
- **Primär**: Web-Applikation (Browser-basiert, keine Installation notwendig)
- **Sekundär**: Mobile-Web (responsive) für Tablets und Smartphones
- **Optional**: Native App (iOS/Android) für spezifische Funktionen (Kampfaufruf, Schiedsrichter-Interface)

### 4.2 Datenbank
- **Primär**: PostgreSQL (Cloud-gehostet) für Produktivbetrieb
- **Lokal/Offline**: SQLite als lokale Fallback-Option
- **Caching**: Redis für Echtzeit-Daten und Session-Management

### 4.3 Infrastruktur
- Hosting auf einem Cloud-Anbieter (z. B. AWS, Azure, Hetzner)
- Container-basierte Deployments (Docker/Kubernetes)
- CI/CD-Pipeline für automatisierte Tests und Deployments

### 4.4 Browser-Kompatibilität
- Chrome (letzte 2 Versionen)
- Firefox (letzte 2 Versionen)
- Safari (letzte 2 Versionen)
- Edge (letzte 2 Versionen)

---

## 5. Randbedingungen

- Das Tool muss auch unter schlechten WLAN-Bedingungen (Sporthallen) funktionieren.
- Einfache Installation und Konfiguration vor Ort durch technisch nicht versierte Personen.
- Budgetrahmen für die Entwicklung: noch zu definieren.
- Zeitplan: MVP (Minimum Viable Product) innerhalb von 6 Monaten.
