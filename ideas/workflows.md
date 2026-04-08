# Wettkampfabläufe (Workflows)

Diese Datei beschreibt die detaillierten Abläufe und Prozesse innerhalb eines Ringkampfsport-Wettbewerbs.

## 1. Teilnehmerregistrierung

### Vor dem Turnier
1. Turnierverwaltung erstellt die Veranstaltung im System (Datum, Ort, Disziplin, Gewichtsklassen).
2. Vereine melden ihre Athleten online oder per Importdatei an.
3. Das System prüft automatisch Pflichtfelder (Name, Geburtsdatum, Verein, Gewichtsklasse, Lizenz).
4. Bei fehlenden oder ungültigen Daten wird der Verein per E-Mail benachrichtigt.
5. Die Anmeldefrist wird überwacht; nach Ablauf sind keine Änderungen mehr möglich (außer durch den Administrator).
6. Das System generiert automatisch eine vorläufige Startliste und sendet diese zur Bestätigung.

### Am Wettkampftag (Einwiegen)
1. Athleten melden sich am Einwiegestand.
2. Wiege-Ergebnis wird im System erfasst und mit der gemeldeten Gewichtsklasse abgeglichen.
3. Bei Übergewicht: Der Athlet hat eine definierte Zeitspanne zum Nachwiegen.
4. Bei Startberechtigung: Bestätigung im System → Athlet wird als „eingewogen" markiert.
5. Die endgültige Startliste wird erstellt und an das Kampfgericht übergeben.

---

## 2. Kampfplanung & Auslosung

1. Nach Ablauf der Einwiegephase startet die automatische Auslosung.
2. Das System gruppiert Athleten nach Gewichtsklasse und Altersgruppe.
3. Je nach Turniermodus (Einzel-KO, Doppel-KO, Round-Robin) erstellt das System die Paarungen.
4. Athleten desselben Vereins werden in frühen Runden automatisch getrennt (wenn möglich).
5. Gesetzte Athleten (Seedung) werden entsprechend ihrer Platzierung in den Bracket eingesetzt.
6. Der Administrator kann Paarungen manuell anpassen und bestätigen.
7. Kämpfe werden auf die vorhandenen Matten/Arenen und Zeitslots verteilt.
8. Der finale Kampfplan wird ausgegeben (Druck, PDF, Bildschirmanzeige).

---

## 3. Kampfstart

1. Kampfaufruf: Das System zeigt den nächsten Kampf auf der Anzeige und benachrichtigt ggf. per App.
2. Der Schiedsrichter bestätigt den Kampfstart im System (Tablet/PC).
3. Der Kampftimer wird gestartet (je nach Regelwerk: z. B. 5 Minuten für Senioren).
4. Punkte und Aktionen werden in Echtzeit erfasst:
   - Punkte für Würfe/Takedowns (1–5 Punkte je nach Technik)
   - Verwarnungen und Strafen
   - Passivitätsregel (gelbe Karte)
5. Bei Sieg durch technische Überlegenheit (z. B. 10 Punkte Vorsprung) endet der Kampf automatisch.

---

## 4. Kampfende & Ergebniserfassung

1. Kampfende durch Ablauf der Zeit, technische Überlegenheit, Aufgabe (Schultersieg) oder Disqualifikation.
2. Das Kampfergebnis (Sieger, Ergebnis-Typ, Punktestand) wird durch den Schiedsrichter bestätigt.
3. Das Kampfgericht überprüft und genehmigt das Ergebnis.
4. Bei Einspruch: Kampf wird als „unter Vorbehalt" markiert; Kampfgericht trifft endgültige Entscheidung.
5. Das Ergebnis wird gespeichert und sofort in der Live-Anzeige aktualisiert.
6. Das Turnier-Bracket wird automatisch aktualisiert (Sieger rückt vor).

---

## 5. Punktevergabe & Rangliste

1. Nach jedem Kampf werden Turnierpunkte gemäß dem gewählten Wertungssystem vergeben:
   - Sieg: 4 Punkte
   - Sieg durch technische Überlegenheit: 5 Punkte
   - Sieg durch Aufgabe/Schultersieg: 5 Punkte
   - Niederlage: 0 Punkte
   - Niederlage durch Disqualifikation: -1 Punkt (optional)
2. Bei Gleichstand entscheiden Hilfskriterien (z. B. Kopf-an-Kopf-Ergebnis, weniger Niederlagen).
3. Die aktuelle Rangliste ist jederzeit im System einsehbar.
4. Nach Abschluss aller Kämpfe einer Gewichtsklasse wird die endgültige Platzierung bestimmt.
5. Pokalplätze (1.–3.) werden für die Siegerehrung vorgemerkt.

---

## 6. Siegerehrung & Abschluss

1. Das System generiert eine endgültige Ergebnisliste pro Gewichtsklasse und Disziplin.
2. Urkunden und Medaillenträger-Listen werden für den Druck vorbereitet.
3. Die Gesamtwertung (Vereinspokal, Teamrangliste) wird berechnet.
4. Ein Turnierbericht (PDF) wird erstellt und exportiert.
5. Alle Ergebnisse werden gespeichert und stehen für zukünftige Statistiken zur Verfügung.

---

## 7. Nachbereitung

1. Ergebnisse werden an Verbände und Organisationen übermittelt (Export).
2. Athleten und Vereine erhalten eine automatische E-Mail mit ihren Ergebnissen.
3. Administrator schließt das Turnier im System ab (Status: „abgeschlossen").
4. Daten bleiben für historische Auswertungen und Statistiken archiviert.
