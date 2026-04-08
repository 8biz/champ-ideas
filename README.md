# champ – Ringkampfsport-Wettbewerbs-Management-Tool

> **Brainstorming & Ideensammlung** für ein Tool zur Leitung von Ringkampfsport-Wettbewerben.

## Projektbeschreibung

**champ** ist ein geplantes Software-Tool zur vollständigen Abwicklung von Ringkampfsport-Wettbewerben. Es unterstützt Wettkampfleiter, Kampfrichter, Vereine und Athleten bei der Organisation und Durchführung von Turnieren – von der Anmeldung bis zur Siegerehrung.

### Geplante Kernfunktionen

- 🏅 **Teilnehmerverwaltung** – Athleten registrieren, Gewichtsklassen zuweisen, Startberechtigung prüfen
- 🥊 **Kampfplanung** – Automatische Paarungserstellung (KO, Doppel-KO, Round-Robin)
- 📊 **Punktevergabe** – Echtzeit-Erfassung von Kampfergebnissen mit Live-Update
- 📺 **Live-Anzeige** – Öffentliche Anzeigetafel für Zuschauer (auch per QR-Code auf dem Handy)
- 📈 **Statistiken** – Vereinswertung, Athleten-Stats, exportierbare Turnierberichte

---

## Repository-Struktur

```
champ-ideas/
├── ideas/
│   ├── features.md         # Liste aller geplanten Features
│   ├── workflows.md        # Wettkampfabläufe (Registrierung, Kampf, Auswertung)
│   └── requirements.md     # Technische und funktionale Anforderungen
├── specs/
│   ├── functional_spec.md  # Funktionale Spezifikation: Was soll das Tool leisten?
│   └── technical_spec.md   # Technische Spezifikation: Wie wird das Tool umgesetzt?
├── assets/                 # Bilder, Diagramme, Mockups
└── README.md               # Diese Datei
```

---

## Dokumentation

| Datei | Inhalt |
|-------|--------|
| [ideas/features.md](ideas/features.md) | Alle geplanten Features im Überblick |
| [ideas/workflows.md](ideas/workflows.md) | Detaillierte Wettkampfabläufe |
| [ideas/requirements.md](ideas/requirements.md) | Technische und funktionale Anforderungen |
| [specs/functional_spec.md](specs/functional_spec.md) | Was soll das Tool leisten? |
| [specs/technical_spec.md](specs/technical_spec.md) | Technische Umsetzung (Stack, Architektur, DB) |

---

## Technologie-Stack (geplant)

| Bereich      | Technologie                         |
|--------------|-------------------------------------|
| Frontend     | React.js 18+, TypeScript, Vite      |
| UI           | Tailwind CSS + shadcn/ui            |
| Backend      | Node.js 20+, NestJS, TypeScript     |
| Datenbank    | PostgreSQL (Produktion), SQLite     |
| Cache        | Redis                               |
| Echtzeit     | Socket.io (WebSockets)              |
| Testing      | Jest, Playwright                    |
| CI/CD        | GitHub Actions                      |
| Deployment   | Docker, Hetzner Cloud               |

---

## Mitmachen (Contributing)

Ideen, Verbesserungsvorschläge und Diskussionen sind willkommen!

1. **Ideen einreichen**: Erstelle ein [GitHub Issue](../../issues) mit dem Label `Feature` oder `Enhancement`.
2. **Fehler melden**: Nutze das Label `Bug` bei Issues.
3. **Pull Requests**: Forke das Repository, erstelle einen Feature-Branch und stelle einen Pull Request.

### Branching-Konvention
```
main            – Stabiler Stand
feature/<name>  – Neue Features
fix/<name>      – Bugfixes
docs/<name>     – Dokumentationsänderungen
```

---

## Lizenz

Dieses Projekt steht unter der [MIT-Lizenz](LICENSE).

---

## Kontakt

Projektverantwortlich: **8biz**  
GitHub: [https://github.com/8biz/champ-ideas](https://github.com/8biz/champ-ideas)
