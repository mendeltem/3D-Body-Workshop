# Körper·Werkstatt 🧊 — 3D Body Workshop

**An interactive 3D learning tool for lower-secondary geometry — explore the volume and surface area of solids, unfold their nets, and practise.**
*Ein interaktives 3D-Lernwerkzeug für Geometrie der Sekundarstufe I — Volumen und Oberfläche von Körpern entdecken, Netze auffalten und üben.*

Everything lives in **a single HTML file**: no server, no build, no install. Works offline and is bilingual (English / German).

### 🔗 Live demo / Live-Demo: **https://mendeltem.github.io/3D-Body-Workshop/**

> *Created by Uchralt Temuulen — feedback welcome / Feedback willkommen: [LinkedIn](https://www.linkedin.com/in/uchralt-temuulen-31a3a570)*

**Language / Sprache:** [🇬🇧 English](#-english) · [🇩🇪 Deutsch](#-deutsch) · [📚 References / Quellen](#-references--wissenschaftliche-grundlagen)

---

## 🇬🇧 English

### Overview

The app has three modes, switchable via the tabs at the top:

**1. Explore — build & measure**
- Drop solids from the library into a freely rotatable 3D scene, combine them, and change dimensions via sliders **or direct numeric input**.
- Live-updating **formulas with intermediate steps** (V and O) plus a result overlay.
- **"Why is that?"** explains where each formula comes from (e.g. why pyramid/cone carry the ⅓).
- **Cross-section** with a height slider: slices the solid and shows the cross-sectional area — making the ⅓ and the "base area × height" idea visible.

**2. Net & Area — unfold**
- Animated **unfolding** of the solid's net.
- Tap each face — the individual areas visibly add up to the total **surface area O**.

**3. Test — questions**
- Two modes: **Test** (timed, scored) or **Practice** (no time pressure, unlimited attempts).
- Difficulty **levels 1–3**, plus **Rising** or **Adaptive**.
- Choose **10 / 20 / 30** questions; ask for **V, O, or mixed**; includes **reverse questions** (rearrange the formula).
- **Diagnostic feedback**: detects common mistakes from the entered number and explains them — forgot the ⅓, mixed up radius/diameter, computed O instead of V, wrong order of magnitude.
- **Staged hints** (💡): first the formula, then the full **step-by-step solution**.
- **Weakness statistics** at the end (accuracy per solid) + a **"Practice weakest solids"** button.
- **Retry the wrong ones** as a bonus round.
- Points, streaks, stars and badges.

**Supported solids:** cube · cuboid · (triangular) prism · cylinder · pyramid · cone · sphere

### Classroom use

The Test tab has fields for the **student's name** and the **teacher's e-mail** (stored locally in the browser). At the end of a test:
1. **Download PDF + JSON** (filename = name + date).
2. **Open mail app** (a real `mailto:` link) — or **Open Gmail in the browser** if no mail app is installed.
3. Attach the two downloaded files in the e-mail and send.

> ⚠️ For security reasons a static web page **cannot attach files to an e-mail automatically** — download first, then attach manually. (A sphere, by the way, has no real net; see the note in the Net tab.)

**Analysing results (Python / pandas)** — put all JSON files in one folder:

```python
import pandas as pd, json, glob

rows = [json.load(open(f, encoding="utf-8")) for f in glob.glob("*.json")]

df   = pd.json_normalize(rows)                                   # one row per student
df_q = pd.json_normalize(rows, "questions",
        ["student", "date", "difficulty", "mode"])               # one row per question
```

### Getting started

**Locally:** download `index.html` and open it in a browser (double-click).
**Offline?** Yes — except the **PDF export** (loads jsPDF from a CDN). JSON export always works.

**Online via GitHub Pages**
1. The app must be named **`index.html`** in the repo (otherwise the URL shows a 404 — Pages always looks for `index.html` first).
2. **Settings → Pages → Source: "Deploy from a branch" → Branch: `main` / `/ (root)` → Save**.
3. After a minute the app is live at the URL above.

### Tech
- **Vanilla JavaScript**, one single `.html` file (HTML + CSS + JS inline).
- **[Three.js](https://threejs.org/) r128** for 3D (custom orbit control, no addon).
- **[jsPDF](https://github.com/parallax/jsPDF) 2.5.1** for PDF export.
- Inline SVG for the nets. No frameworks, no build step, no dependencies to install.
- Built-in error overlay: runtime errors are shown on-screen (handy for bug reports).

### Notes & limits
- **Browser storage:** name and teacher e-mail are kept only locally via `localStorage` — nothing is uploaded.
- The **diagnostic feedback** catches the most common error types, not every arithmetic slip.
- A **sphere has no flat net**; the four great circles shown are a magnitude aid, not an unfoldable net.

---

## 🇩🇪 Deutsch

### Überblick

Die App hat drei Modi, umschaltbar über die Reiter oben:

**1. Entdecken — bauen & messen**
- Körper aus der Bibliothek in einen frei drehbaren 3D-Raum legen, kombinieren und Maße per Schieberegler **oder direkter Zahleneingabe** ändern.
- Live aktualisierte **Formeln mit Zwischenschritten** (V und O) plus Ergebnis-Overlay.
- **„Warum gilt das?"** erklärt die Herkunft jeder Formel (z. B. warum bei Pyramide/Kegel das ⅓ steht).
- **Querschnitt** mit Höhen-Schieber: schneidet den Körper und zeigt die Querschnittsfläche — macht das ⅓ und das Prinzip „Grundfläche × Höhe" sichtbar.

**2. Netz & Fläche — aufklappen**
- Animiertes **Auffalten** des Körpernetzes.
- Jede Fläche antippen — die Einzelflächen addieren sich sichtbar zur gesamten **Oberfläche O**.

**3. Test — Aufgaben**
- Zwei Betriebsarten: **Test** (mit Zeit & Punkten) oder **Üben** (ohne Zeitdruck, beliebig viele Versuche).
- Schwierigkeit **Stufe 1–3**, dazu **Ansteigend** oder **Adaptiv**.
- Aufgabenzahl **10 / 20 / 30** wählbar; Frage nach **V, O oder gemischt**; auch **Rückwärtsaufgaben** (Formel umstellen).
- **Diagnostisches Feedback**: erkennt typische Fehler an der eingegebenen Zahl und erklärt sie — ⅓ vergessen, Radius/Durchmesser verwechselt, O statt V, falsche Größenordnung.
- **Gestufte Tipps** (💡): erst die Formel, dann die volle **Schritt-für-Schritt-Lösung**.
- **Schwächen-Statistik** am Ende (Trefferquote pro Körper) + Knopf **„Schwächste Körper üben"**.
- **Falsche wiederholen** als Bonusrunde.
- Punkte, Serien (Streak), Sterne und Abzeichen.

**Unterstützte Körper:** Würfel · Quader · Prisma (dreieckig) · Zylinder · Pyramide · Kegel · Kugel

### Einsatz im Unterricht

Im Test-Tab gibt es Felder für **Name** der Schüler:in und **E-Mail der Lehrkraft** (werden lokal im Browser gemerkt). Am Ende des Tests:
1. **PDF + JSON herunterladen** (Dateiname = Name + Datum).
2. **E-Mail-App öffnen** (echter `mailto:`-Link) — oder **Gmail im Browser öffnen**, falls keine Mail-App installiert ist.
3. Die zwei heruntergeladenen Dateien in der E-Mail anhängen und absenden.

> ⚠️ Aus Sicherheitsgründen kann eine reine Webseite **keine Dateien automatisch an eine E-Mail anhängen** — erst herunterladen, dann manuell anhängen. (Eine Kugel hat übrigens kein echtes Netz; siehe Hinweis im Netz-Tab.)

**Ergebnisse auswerten (Python / pandas)** — alle JSON in einen Ordner legen:

```python
import pandas as pd, json, glob

rows = [json.load(open(f, encoding="utf-8")) for f in glob.glob("*.json")]

df   = pd.json_normalize(rows)                                   # eine Zeile pro Schüler:in
df_q = pd.json_normalize(rows, "questions",
        ["student", "date", "difficulty", "mode"])               # eine Zeile pro Aufgabe
```

### Loslegen

**Lokal:** `index.html` herunterladen und im Browser öffnen (Doppelklick).
**Offline?** Ja — bis auf den **PDF-Export** (lädt jsPDF vom CDN). Der JSON-Export funktioniert immer.

**Online über GitHub Pages**
1. Die App muss als **`index.html`** im Repo liegen (sonst zeigt die Adresse einen 404 — GitHub Pages sucht immer zuerst `index.html`).
2. **Settings → Pages → Source: „Deploy from a branch" → Branch: `main` / `/ (root)` → Save**.
3. Nach ein paar Minuten läuft die App unter der obigen Adresse.

### Technik
- **Vanilla JavaScript**, eine einzige `.html`-Datei (HTML + CSS + JS inline).
- **[Three.js](https://threejs.org/) r128** für die 3D-Darstellung (eigene Orbit-Steuerung, kein Addon).
- **[jsPDF](https://github.com/parallax/jsPDF) 2.5.1** für den PDF-Export.
- Inline-SVG für die Netze. Keine Frameworks, kein Build-Schritt, keine Abhängigkeiten.
- Eingebautes Fehler-Overlay: Laufzeitfehler werden sichtbar gemeldet (gut zum Melden von Bugs).

### Hinweise & Grenzen
- **Browser-Speicher:** Name und Lehrer-E-Mail werden via `localStorage` nur lokal auf dem Gerät gespeichert — nichts wird hochgeladen.
- Das **diagnostische Feedback** fängt die häufigsten Fehlertypen ab, aber nicht jeden Rechenfehler.
- Eine **Kugel hat kein ebenes Netz**; die vier gezeigten Großkreise sind eine Größen-Merkhilfe, kein auffaltbares Netz.

---

## 📚 References / Wissenschaftliche Grundlagen

The instructional design is grounded in the following findings. All DOIs were verified.
*Die didaktischen Entscheidungen stützen sich auf folgende Befunde. Alle DOIs wurden geprüft.*

| Source / Quelle | Supports / Begründet |
|---|---|
| Hattie, J. & Timperley, H. (2007). *The Power of Feedback.* Review of Educational Research, 77(1), 81–112. [DOI](https://doi.org/10.3102/003465430298487) | **EN:** Diagnostic feedback works best when it targets the task/process and explains *why* — not just "right/wrong". · **DE:** Diagnostisches Feedback: wirksam, wenn es auf Aufgabe/Lösungsweg zielt und *warum* erklärt. |
| Black, P. & Wiliam, D. (1998). *Assessment and Classroom Learning.* Assessment in Education, 5(1), 7–74. [DOI](https://doi.org/10.1080/0969595980050102) | **EN:** Formative assessment with immediate feedback substantially improves learning → practice mode & weakness stats. · **DE:** Formatives Prüfen mit sofortiger Rückmeldung → Übungsmodus & Schwächen-Statistik. |
| Sweller, J. (1988). *Cognitive Load During Problem Solving.* Cognitive Science, 12(2), 257–285. [DOI](https://doi.org/10.1207/s15516709cog1202_4) | **EN:** Cognitive Load Theory (foundation): search-based problem solving overloads working memory. · **DE:** Cognitive Load Theory (Grundlage): suchendes Problemlösen überlastet das Arbeitsgedächtnis. |
| Sweller, J. & Cooper, G. A. (1985). *The use of worked examples as a substitute for problem solving in learning algebra.* Cognition and Instruction, 2(1), 59–89. [DOI](https://doi.org/10.1207/s1532690xci0201_3) | **EN:** Direct evidence for the step-by-step solution (worked examples). · **DE:** Direkter Beleg für die Schritt-für-Schritt-Lösung (Lösungsbeispiele). |
| Roediger, H. L. & Karpicke, J. D. (2006). *Test-Enhanced Learning.* Psychological Science, 17(3), 249–255. [DOI](https://doi.org/10.1111/j.1467-9280.2006.01693.x) | **EN:** Testing effect: active retrieval beats rereading. · **DE:** Testing-Effekt: aktives Erinnern schlägt Wiederholen. |
| Dunlosky, J. et al. (2013). *Improving Students' Learning With Effective Learning Techniques.* Psychological Science in the Public Interest, 14(1), 4–58. [DOI](https://doi.org/10.1177/1529100612453266) | **EN:** Practice testing & distributed practice → "retry wrong" / "practice weakest". · **DE:** Übungstests & verteiltes Üben → „Falsche wiederholen" / „Schwächste üben". |
| Ashcraft, M. H. & Kirk, E. P. (2001). *Working memory, math anxiety, and performance.* J. Exp. Psychology: General, 130(2), 224–237. [DOI](https://doi.org/10.1037/0096-3445.130.2.224) | **EN:** Math anxiety disrupts working memory. *Inferred* (not directly tested): practice mode without a timer. · **DE:** Mathe-Angst stört das Arbeitsgedächtnis. *Daraus abgeleitet* (nicht direkt geprüft): Übungsmodus ohne Uhr. |
| Ainsworth, S. (2006). *DeFT: Learning with multiple representations.* Learning and Instruction, 16(3), 183–198. [DOI](https://doi.org/10.1016/j.learninstruc.2006.03.001) | **EN:** Linked multiple representations: 3D solid, net, formula, cross-section. · **DE:** Verknüpfte Mehrfachdarstellungen: 3D-Körper, Netz, Formel, Querschnitt. |
| Van Hiele, P. M. (1986). *Structure and Insight.* Academic Press. [Overview](https://en.wikipedia.org/wiki/Van_Hiele_model) | **EN:** Geometric thinking in levels: explore visually first, then formalise. · **DE:** Geometrisches Denken in Stufen: erst anschaulich erkunden, dann formalisieren. |
| Cavalieri's principle (B. Cavalieri, 1635). [Overview](https://en.wikipedia.org/wiki/Cavalieri%27s_principle) | **EN:** Mathematical basis of the cross-section view: equal cross-sections ⇒ equal volume. · **DE:** Mathematische Basis der Querschnitt-Ansicht: gleiche Querschnitte ⇒ gleiches Volumen. |

> **Units / Einheiten:** generic units are used — VE (volume unit / Volumeneinheit), FE (area unit / Flächeneinheit), LE (length unit / Längeneinheit) — following the convention of many lower-secondary textbooks.

---

## 🤝 Contributing & Feedback / Mitwirken

Ideas, bugs or suggestions via [Issues](../../issues) or directly:
**[Uchralt Temuulen · LinkedIn](https://www.linkedin.com/in/uchralt-temuulen-31a3a570)**

## 📄 License / Lizenz

To be decided — **MIT** recommended (free for educational use). *Noch festzulegen — MIT empfohlen (frei für den Bildungseinsatz).*
