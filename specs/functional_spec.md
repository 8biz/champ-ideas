# Funktionale Spezifikation

**Projekt**: champ – Ringkampfsport-Wettbewerbs-Management-Tool  
**Version**: 0.1.0 (Entwurf)  
**Stand**: 2026-04-08  

---

## 1. Einleitung

### 1.1 Zweck
Diese funktionale Spezifikation beschreibt, **was** das Tool leisten soll. Sie richtet sich an alle Stakeholder – Entwickler, Auftraggeber, Vereine und Kampfgericht – und dient als Grundlage für die technische Umsetzung.

### 1.2 Umfang
Das Tool unterstützt die vollständige Abwicklung eines Ringkampfsport-Wettbewerbs: von der Anmeldung der Athleten bis zur Siegerehrung und Nachbereitung.

---

## 2. Systemübersicht

Das System besteht aus folgenden Hauptmodulen:

| Modul                | Beschreibung                                                    |
|----------------------|-----------------------------------------------------------------|
| Turnierverwaltung    | Erstellen und Konfigurieren von Turnieren                       |
| Teilnehmerverwaltung | Erfassung, Verwaltung und Einteilung der Athleten               |
| Kampfplanung         | Automatische Erstellung und Verwaltung von Kampfpaarungen       |
| Kampfdurchführung    | Echtzeit-Erfassung von Kampfergebnissen                         |
| Live-Anzeige         | Öffentliche Anzeige von Kämpfen, Ergebnissen und Ranglisten     |
| Statistik & Export   | Auswertungen, Berichte und Datenexport                          |
| Benutzerverwaltung   | Rollen, Rechte und Authentifizierung                            |

---

## 3. Detaillierte Funktionsbeschreibungen

### 3.1 Turnierverwaltung

**Funktion**: Turnier anlegen  
Das System ermöglicht Administratoren, ein neues Turnier mit folgenden Angaben anzulegen:
- Name, Datum, Ort, Veranstalter
- Disziplin (Freistil, Greco-Römisch, Judo, Sambo, ...)
- Gewichtsklassen und Altersgruppen
- Turniermodus (KO, Doppel-KO, Round-Robin)
- Anmeldefrist und maximale Teilnehmerzahl

**Funktion**: Turnier verwalten  
Administratoren können Turnierdaten bis zum Start bearbeiten, Phasen wechseln (Anmeldung → Einwiegen → Wettkampf → Abschluss) und das Turnier abschließen.

---

### 3.2 Teilnehmerverwaltung

**Funktion**: Athlet registrieren  
Vereine oder Administratoren können Athleten mit folgenden Daten erfassen:
- Vorname, Nachname, Geburtsdatum, Geschlecht
- Verein, Verbandsnummer/Lizenz
- Gewichtsklasse, Disziplin
- Optionales Profilfoto

**Funktion**: Athleten in Gewichtsklassen einteilen  
- Das System teilt Athleten automatisch in die passende Gewichtsklasse ein (basierend auf gemeldetem Gewicht).
- Am Einwiegetag werden die tatsächlichen Gewichtswerte erfasst und abgeglichen.
- Athleten, die das Gewichtslimit überschreiten, werden als „nicht startberechtigt" markiert.

**Funktion**: Startliste verwalten  
- Das System erstellt eine vorläufige und endgültige Startliste.
- Import aus CSV/Excel für Massenanmeldungen.
- Export der Startliste als PDF oder Excel.

---

### 3.3 Kampfplanung

**Funktion**: Kampfpaarungen automatisch erstellen  
- Nach Abschluss der Einwiegephase erstellt das System automatisch die Kampfpaarungen.
- Athleten desselben Vereins werden in frühen Runden getrennt.
- Gesetzte Athleten werden korrekt platziert.
- Unterstützte Turniermodi:
  - **Einzel-KO (Single Elimination)**: Jeder Verlierer scheidet aus.
  - **Doppel-KO (Double Elimination)**: Zwei Niederlagen führen zum Ausscheiden.
  - **Round-Robin (Jeder gegen Jeden)**: Alle kämpfen gegen alle; Rangliste nach Punkten.

**Funktion**: Kampfplan erstellen  
- Kämpfe werden auf verfügbare Matten und Zeitslots verteilt.
- Das System optimiert den Kampfplan, um Wartezeiten zu minimieren.
- Manuelle Anpassungen durch den Administrator sind möglich.

---

### 3.4 Kampfdurchführung

**Funktion**: Kampf starten  
- Der Schiedsrichter ruft den Kampf im System auf und bestätigt den Start.
- Der Kampftimer startet automatisch (konfigurierbare Kampfdauer je Altersgruppe).

**Funktion**: Punkte erfassen  
- In Echtzeit werden Punkte für Würfe, Takedowns und andere Techniken eingegeben.
- Verwarnungen und Strafen werden erfasst.
- Passive Aktionen werden mit Gelber/Roter Karte bewertet.

**Funktion**: Kampf beenden  
- Kampfende durch: Ablauf der Zeit, technische Überlegenheit, Aufgabe (Schultersieg), Disqualifikation.
- Das Ergebnis wird durch das Kampfgericht bestätigt.
- Einsprüche können innerhalb einer definierten Zeit erhoben werden.

---

### 3.5 Live-Anzeige

**Funktion**: Öffentliche Anzeigetafel  
- Alle laufenden und nächsten Kämpfe werden auf einem öffentlichen Dashboard angezeigt.
- Aktualisierung in Echtzeit ohne Seitenneuladen (WebSocket-basiert).
- Zuschauer können die Anzeige per QR-Code auf ihrem Smartphone aufrufen.

**Funktion**: Scoreboard-Modus  
- Großbildschirm-Ansicht für eine einzelne Matte mit Punktestand und Timer.
- Geeignet für Anzeigetafeln in der Halle.

---

### 3.6 Statistik & Export

**Funktion**: Auswertungen generieren  
- Turnierstatistiken: Anzahl Kämpfe, Ergebnistypen, durchschnittliche Kampfdauer.
- Athleten-Statistiken: Siege, Niederlagen, Punktedurchschnitt.
- Vereinswertung und Teamrangliste.

**Funktion**: Daten exportieren  
- Ergebnislisten als PDF oder Excel.
- Urkunden-Vorlage für Siegerehrung.
- Rohdaten-Export für Verbände (CSV).

---

### 3.7 Benutzerverwaltung

**Funktion**: Benutzerverwaltung  
Folgende Rollen sind vorgesehen:

| Rolle           | Rechte                                                         |
|-----------------|----------------------------------------------------------------|
| Administrator   | Vollzugriff; Turnier, Nutzer, alle Einstellungen               |
| Kampfgericht    | Ergebnisse bestätigen, Einsprüche entscheiden                  |
| Schiedsrichter  | Kampf starten/beenden, Punkte eingeben                         |
| Vereinsvertreter| Athleten anmelden, eigene Daten einsehen                       |
| Öffentlichkeit  | Nur-Lesen: Live-Anzeige, Ergebnisse                            |

---

## 4. Abgrenzung (Nicht im Scope)

- Keine Videoschnitt- oder Streamingfunktion.
- Keine Verwaltung von Trainingseinheiten oder Vereinsmanagement außerhalb des Turniers.
- Keine direkte Anbindung an externe Zahlungsdienstleister für Startgelder (kann später ergänzt werden).
