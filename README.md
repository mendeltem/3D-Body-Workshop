# Körper·Werkstatt 🧊

**Ein interaktives 3D-Lernwerkzeug für Geometrie der Sekundarstufe I — Volumen und Oberfläche von Körpern entdecken, Netze auffalten und üben.**

Alles steckt in **einer einzigen HTML-Datei**: kein Server, kein Build, keine Installation. Datei öffnen — fertig. Funktioniert offline, ist zweisprachig (Deutsch / Englisch) und für den Klassenraum gedacht.

### 🔗 Live-Demo: **https://mendeltem.github.io/3D-Body-Workshop/**

> *Created by Uchralt Temuulen — Feedback willkommen: [LinkedIn](https://www.linkedin.com/in/uchralt-temuulen-31a3a570)*

---

## ✨ Überblick

Die App hat drei Modi, umschaltbar über die Reiter oben:

### 1. Entdecken 🔍 — bauen & messen
- Körper aus der Bibliothek in einen frei drehbaren 3D-Raum legen, kombinieren und Maße per Schieberegler **oder direkter Zahleneingabe** ändern.
- Live aktualisierte **Formeln mit Zwischenschritten** (V und O) plus Ergebnis-Overlay.
- **„Warum gilt das?"** — erklärt die Herkunft jeder Formel (z. B. warum bei Pyramide/Kegel das ⅓ steht).
- **Querschnitt** mit Höhen-Schieber: schneidet den Körper und zeigt die Querschnittsfläche — macht das ⅓ und das Prinzip „Grundfläche × Höhe" sichtbar.

### 2. Netz & Fläche 📐 — aufklappen
- Körpernetz mit animiertem **Auffalten**.
- Jede Fläche antippen — die Einzelflächen addieren sich sichtbar zur gesamten **Oberfläche O**.

### 3. Test 📝 — Aufgaben
- Zwei Betriebsarten: **Test** (mit Zeit & Punkten) oder **Üben** (ohne Zeitdruck, beliebig viele Versuche).
- Schwierigkeit **Stufe 1–3**, dazu **Ansteigend** oder **Adaptiv**.
- Aufgabenzahl **10 / 20 / 30** wählbar; Frage nach **V, O oder gemischt**; auch **Rückwärtsaufgaben** (Formel umstellen).
- **Diagnostisches Feedback**: erkennt typische Fehler an der eingegebenen Zahl und erklärt sie — ⅓ vergessen, Radius/Durchmesser verwechselt, O statt V, falsche Größenordnung.
- **Gestufte Tipps** (💡): erst die Formel, dann die volle **Schritt-für-Schritt-Lösung**.
- **Schwächen-Statistik** am Ende (Trefferquote pro Körper) + Knopf **„Schwächste Körper üben"**.
- **Falsche wiederholen** als Bonusrunde.
- Punkte, Serien (Streak), Sterne und Abzeichen.

### Unterstützte Körper
Würfel · Quader · Prisma (dreieckig) · Zylinder · Pyramide · Kegel · Kugel

---

## 🎓 Einsatz im Unterricht

Im Test-Tab gibt es Felder für **Name** der Schüler:in und **E-Mail der Lehrkraft** (werden lokal im Browser gemerkt). Am Ende des Tests:

- **„Ergebnisse per E-Mail senden"** lädt **PDF + JSON** herunter (Dateiname = Name + Datum) und öffnet die E-Mail-App mit fertigem Empfänger, Betreff und Text. Die zwei Dateien müssen noch angehängt werden.
- **PDF** = lesbares Protokoll; **JSON** = maschinenlesbar zum Sammeln und Auswerten.

> ⚠️ **Hinweis:** Aus Sicherheitsgründen kann eine reine HTML-Seite keine E-Mail mit Anhang *automatisch* versenden — die Dateien werden heruntergeladen und manuell angehängt.

### Ergebnisse auswerten (Python / pandas)

Alle JSON in einen Ordner legen, dann:

```python
import pandas as pd, json, glob

rows = [json.load(open(f, encoding="utf-8")) for f in glob.glob("*.json")]

df   = pd.json_normalize(rows)                                   # eine Zeile pro Schüler:in
df_q = pd.json_normalize(rows, "questions",
        ["student", "date", "difficulty", "mode"])               # eine Zeile pro Aufgabe
```

---

## 🚀 Loslegen

**Lokal:** `index.html` herunterladen und im Browser öffnen (Doppelklick). Das war's.

**Offline?** Ja — bis auf den **PDF-Export** (lädt die jsPDF-Bibliothek vom CDN) braucht nichts eine Internetverbindung. Der JSON-Export funktioniert immer.

### Online über GitHub Pages
1. Die App muss als **`index.html`** im Repo liegen (sonst zeigt die Adresse einen 404 — GitHub Pages sucht am Anfang immer `index.html`).
2. **Settings → Pages → Source: „Deploy from a branch" → Branch: `main` / `/ (root)` → Save**.
3. Nach ein paar Minuten läuft die App unter:
   **https://mendeltem.github.io/3D-Body-Workshop/**

---

## 🛠️ Technik

- **Vanilla JavaScript**, eine einzige `.html`-Datei (HTML + CSS + JS inline).
- **[Three.js](https://threejs.org/) r128** für die 3D-Darstellung (eigene Orbit-Steuerung, kein Addon).
- **[jsPDF](https://github.com/parallax/jsPDF) 2.5.1** für den PDF-Export.
- Inline-SVG für die Netze.
- Keine Frameworks, kein Build-Schritt, keine Abhängigkeiten zum Installieren.
- Eingebautes Fehler-Overlay: Laufzeitfehler werden sichtbar gemeldet (gut zum Melden von Bugs).

---

## 🔬 Wissenschaftliche Grundlagen

Die didaktischen Entscheidungen stützen sich auf Befunde der Lern- und Mathematikdidaktik-Forschung. Alle DOIs wurden geprüft.

| Quelle | Begründet |
|---|---|
| Hattie, J. & Timperley, H. (2007). *The Power of Feedback.* Review of Educational Research, 77(1), 81–112. [DOI](https://doi.org/10.3102/003465430298487) | Diagnostisches Feedback: wirksam, wenn es auf Aufgabe/Lösungsweg zielt — nicht nur „richtig/falsch". |
| Black, P. & Wiliam, D. (1998). *Assessment and Classroom Learning.* Assessment in Education, 5(1), 7–74. [DOI](https://doi.org/10.1080/0969595980050102) | Formatives Prüfen mit sofortiger Rückmeldung → Übungsmodus & Schwächen-Statistik. |
| Sweller, J. (1988). *Cognitive Load During Problem Solving.* Cognitive Science, 12(2), 257–285. [DOI](https://doi.org/10.1207/s15516709cog1202_4) | Cognitive Load Theory (Grundlage): suchendes Problemlösen überlastet das Arbeitsgedächtnis. |
| Sweller, J. & Cooper, G. A. (1985). *The use of worked examples as a substitute for problem solving in learning algebra.* Cognition and Instruction, 2(1), 59–89. [DOI](https://doi.org/10.1207/s1532690xci0201_3) | Direkter Beleg für die Schritt-für-Schritt-Lösung (Lösungsbeispiele). |
| Roediger, H. L. & Karpicke, J. D. (2006). *Test-Enhanced Learning.* Psychological Science, 17(3), 249–255. [DOI](https://doi.org/10.1111/j.1467-9280.2006.01693.x) | Testing-Effekt: aktives Erinnern festigt Wissen stärker als Wiederholen. |
| Dunlosky, J. et al. (2013). *Improving Students' Learning With Effective Learning Techniques.* Psychological Science in the Public Interest, 14(1), 4–58. [DOI](https://doi.org/10.1177/1529100612453266) | Übungstests & verteiltes Üben → „Falsche wiederholen" / „Schwächste üben". |
| Ashcraft, M. H. & Kirk, E. P. (2001). *Working memory, math anxiety, and performance.* J. Exp. Psychology: General, 130(2), 224–237. [DOI](https://doi.org/10.1037/0096-3445.130.2.224) | Mathe-Angst stört das Arbeitsgedächtnis. *Daraus abgeleitet* (nicht direkt geprüft): Übungsmodus ohne Uhr. |
| Ainsworth, S. (2006). *DeFT: Learning with multiple representations.* Learning and Instruction, 16(3), 183–198. [DOI](https://doi.org/10.1016/j.learninstruc.2006.03.001) | Verknüpfte Mehrfachdarstellungen: 3D-Körper, Netz, Formel, Querschnitt. |
| Van Hiele, P. M. (1986). *Structure and Insight: A Theory of Mathematics Education.* Academic Press. [Übersicht](https://en.wikipedia.org/wiki/Van_Hiele_model) | Geometrisches Denken in Stufen: erst anschaulich erkunden, dann formalisieren. |
| Prinzip von Cavalieri (B. Cavalieri, 1635). [Übersicht](https://de.wikipedia.org/wiki/Prinzip_von_Cavalieri) | Mathematische Basis der Querschnitt-Ansicht: gleiche Querschnitte ⇒ gleiches Volumen. |

> Hinweis zu Einheiten: Es werden generische Einheiten verwendet (VE = Volumeneinheit, FE = Flächeneinheit, LE = Längeneinheit), wie in vielen Lehrwerken der Sekundarstufe I.

---

## 📋 Hinweise & Grenzen

- **Browser-Speicher:** Name und Lehrer-E-Mail werden via `localStorage` nur lokal auf dem Gerät gespeichert — nichts wird hochgeladen.
- **E-Mail-Versand** öffnet die Standard-E-Mail-App des Geräts; Anhänge müssen manuell hinzugefügt werden.
- Das **diagnostische Feedback** fängt die häufigsten Fehlertypen ab, aber nicht jeden Rechenfehler.

---

## 🤝 Mitwirken & Feedback

Hinweise, Fehler oder Ideen gern über die [Issues](../../issues) oder direkt an
**[Uchralt Temuulen · LinkedIn](https://www.linkedin.com/in/uchralt-temuulen-31a3a570)**.

---

## 📄 Lizenz

Noch festzulegen — empfohlen: **MIT** (frei für den Bildungseinsatz). Eine `LICENSE`-Datei kann bei Bedarf ergänzt werden.

---

<sub>English summary: **Körper·Werkstatt** is a single-file, offline-capable, bilingual (DE/EN) 3D web tool for learning the volume and surface area of solids in lower-secondary geometry. Three modes — Explore (build & measure in 3D, with cross-sections and "why" explanations), Net & Area (unfold and sum faces), and Test (timed or untimed practice with diagnostic feedback, step-by-step worked solutions, weakness stats, and PDF/JSON export for classroom use). Built with vanilla JS, Three.js r128 and jsPDF. Grounded in cited learning-science research (see table above).</sub>
