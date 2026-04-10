# NABOKOV — Zielarchitektur
*Mehrprojekt-Prosa-App · Short-Story + Roman/Prosa*

Version: 1.1 — 10.04.2026  
Basis: KERIM APP MASTER REFERENZ v1.0, index_v6_fonts.html, rilke (1).html, Novel Factory Deep Research, Antonya Nelson 9 Schritte  
Gilt für: alle zukünftigen Patches und Erweiterungen an der Nabokov App

---

## INHALT

1. [Kernurteil](#1-kernurteil)
2. [Asset-Bewertung](#2-asset-bewertung)
3. [Novel Factory — Übernahme / Vereinfachung / Verwerfung](#3-novel-factory--übernahme--vereinfachung--verwerfung)
4. [Gemeinsamer Datenkern](#4-gemeinsamer-datenkern)
5. [Mehrprojektmodell](#5-mehrprojektmodell)
6. [Short-Story-Modus](#6-short-story-modus)
7. [Prosa-/Roman-Modus](#7-prosa-roman-modus)
8. [Screen- und Tab-Architektur](#8-screen--und-tab-architektur)
9. [Workflow-/Roadmap-Schicht](#9-workflow-roadmap-schicht)
10. [Migrationsplan in Phasen](#10-migrationsplan-in-phasen)
11. [Technische Risiken / Konflikte](#11-technische-risiken--konflikte)
12. [Erster nächster Build-Schritt](#12-erster-nächster-build-schritt)

---

## 1. Kernurteil

Die App ist eine **persönliche kreative Werkbank für constraint-basiertes und fragmentarisches Prosaschreiben**. Sie verbindet zwei Modi über einen gemeinsamen Datenkern:

- **Short-Story-Modus:** Geführt, constraint-basiert, auf Basis von Antonya Nelsons 9-Schritte-Methode. Kompakt, entscheidungsorientiert, kurzformtauglich. Jeder Schritt ist eine echte Arbeitsstation mit Leitfragen, Rohnotizen, verdichteten Entscheidungen und Varianten.
- **Prosa-/Roman-Modus:** Offen, material- und extraktionsorientiert. Geeignet für fragmentarisches, diktatbasiertes, dialogisches Arbeiten. Übergang von Rohmaterial → Zettel/Karten → Struktur → Draft.

Der Unterschied zwischen den Modi liegt nicht in der Datenhaltung, sondern in der **Prozessführung und UI-Dichte**. Der Short-Story-Modus verdichtet und constrainiert; der Prosa-Modus sammelt und rekombiniert.

Die bestehende `index_v6_fonts.html` ist eine tragfähige Basis. Der Umbau erfolgt inkrementell durch Einführung eines Projektmodells, Erweiterung der State-Struktur und schrittweisen Ausbau der Modi.

---

## 2. Asset-Bewertung

### 2.1 `index_v6_fonts.html` — Hauptbasis

#### Unbedingt erhalten

- Board-Mechanik mit Gingko-artigem Left-to-Right-Spaltenmodell (Nodes als Baum mit Pfadnavigation)
- Node-Datenmodell (`id`, `parentId`, `title`, `text`, `summary`, `beatId`, `splitHistory`, `archived`)
- Entity-System mit Cards-Substruktur (`entities[]` mit `cards[]`)
- Bestehende Framework-/Struktur-Logik als Ausgangsmaterial für das spätere Workflow-System
- OpenAI-Split-Logik inkl. Prompt-Bau, Import-Modal, heuristischem Fallback
- Entity-Cleanup-Workflow (Prompt → Review → Accept)
- Gist-Sync mit Versionscheck, Merge, Vierstufenprotokoll
- Theme-System (dark/light/epaper) und Font-Profile (baskerville/typewriter)
- CSS-Architektur (Variablen, Komponentenklassen, responsive Breakpoints)
- Hilfsfunktionen (`uid`, `esc`, `toast`, `clipCopy`, `githubHeaders`, `openAIHeaders`)

#### Umbaubar, nicht löschbar

- `S.mode` wird von global auf projektbezogen verschoben
- `S.nodes`, `S.entities` und bestehende projektartige Daten werden in ein Projekt-Objekt verschachtelt
- `currentTab` bleibt flüchtiger UI-State
- Settings-Panel wird um Projektverwaltung erweitert

### 2.2 `rilke (1).html` — selektive Übernahme

#### Wertvolle Mechaniken

- **pairRelations** mit `fromCardUid`/`toCardUid`, `positionType`, `note`, `isInteresting` — übertragbar als generisches Relationsmodell zwischen beliebigen Objekten
- **Kompositionskonzept:** Geordnete Liste von Card-UIDs → Vorschau → Export — direkt übertragbar als Kompositions-/Draft-Ansicht
- **Parent/Child-Baumlogik** mit `sid`-Nummerierung — ergänzt die bestehende Node-Baumlogik
- **Brainstorm-Modus** als Entdeckungswerkzeug — konzeptionell nutzbar, aber kein Tag-1-Feature

#### Nicht übernehmen

- Torus-Nachbarschaftslogik (zu spezifisch für Lyrik)
- `matrixSessions` (irrelevant)
- Gesamtes UI-Design (andere Ästhetik, nicht kompatibel mit Nabokov)

### 2.3 Story-Process-Material

- Antonya Nelson 9 Schritte (Notizen + Freeplane-Template + Video-Zusammenfassung) bilden die inhaltliche Grundlage für den Short-Story-Modus
- Die detaillierten Schritt-Erklärungen aus dem Freeplane-Export liefern Leitfragen und Beispiele für die Guided-Step-Ansicht
- Die Buchzusammenfassung liefert die 5 Kernprinzipien (Ticking Clock, Binary Forces, Transitional Situation, Symbolische Objekte, Perspektivwahl) als Constraint-Definitionen

---

## 3. Novel Factory — Übernahme / Vereinfachung / Verwerfung

| NF-Mechanik | Entscheidung | Begründung |
|---|---|---|
| Premise (SCOOD) | **Übernehmen, vereinfacht** | Als optionaler Story-Kern-Block pro Projekt: Freitext + optionale Felder (Figur, Situation, Ziel, Gegenspieler, Katastrophe). Nicht Pflicht. |
| Short Synopsis | **Übernehmen** | Als optionaler One-Pager pro Projekt |
| Extended Synopsis | **Verwerfen für v1** | Erst sinnvoll bei echtem Romanmodus mit mehr Material |
| Plot Manager (Indexkarten) | **Bereits vorhanden** | Board-Mechanik in `index_v6` deckt das ab |
| Goal-to-Decision Cycle | **Verwerfen** | Zu formelhaft, passt nicht zum Fragment-Workflow |
| Subplot Manager | **Verwerfen** | Zu schwergewichtig; stattdessen: Tags/Threads als leichtgewichtige Alternative |
| Scene Blocking | **Übernehmen als Guided Steps** | Im Short-Story-Modus: echte Arbeitsstationen |
| Characters/Locations/Items | **Bereits vorhanden als Entities** | Entity-System erweitern, nicht NF-Panels kopieren |
| Turn Back Time | **Später (Phase 4)** | Versionierung pro Node als späteres Feature |
| Roadmap als Workflow-Schicht | **Übernehmen, abstrahiert** | Workflow = konfigurierbare Schrittfolge pro Modus, verknüpft mit echten Artefakten |
| Statistics | **Später** | Wortanzahl pro Projekt als Low-Priority |
| Adaptive Panel-Anzeige | **Übernehmen als UI-Prinzip** | Nur ausgefüllte Felder anzeigen — gutes Muster für Entity-Detailansichten |
| Character Viewpoint Synopses | **Verwerfen** | Multi-POV-Analyse nur für komplexe Romane |
| Detaillierte Location-Panels | **Verwerfen** | Weltenbau-Superstruktur irrelevant |
| Submission/Publishing-Pipeline | **Verwerfen** | Kein aktuelles Bedürfnis |

---

## 4. Gemeinsamer Datenkern

### 4.1 State-Grundstruktur (neues `S`)

```javascript
var S = {
  version: 3,
  projects: [],            // Array von Project-Objekten
  activeProjectId: '',     // UID des aktuell geöffneten Projekts — local wins bei Merge
  deletedIds: {},          // globale Tombstones (TTL 90 Tage)
  _lastExported: ''
};

// Theme und Font sind gerätelokale Präferenzen.
// Sie werden NICHT in S gespeichert, NICHT synchronisiert.
```

### 4.2 Project

```javascript
Project = {
  id: uid(),
  title: '',
  mode: 'short-story',       // 'short-story' | 'prosa' (| 'poetry' später)
  status: 'active',          // 'idea' | 'active' | 'paused' | 'archived'
  premise: '',               // optionaler Freitext-Kern
  premiseFields: {           // optional, SCOOD-artig
    character: '',
    situation: '',
    objective: '',
    opponent: '',
    disaster: ''
  },
  synopsis: '',              // optionaler One-Pager
  nodes: [],                 // DraftNode[]
  entities: [],              // Entity[]
  relations: [],             // Relation[]
  compositions: [],          // Composition[]
  workflow: {                // einzige Prozessschicht (absorbiert das alte structures-Konzept)
    templateId: 'nelson-9',  // 'nelson-9' | 'generic-9' | 'roman-roadmap' | 'frei'
    steps: []                // WorkflowStep[]
  },
  sources: [],               // SourceDocument[]
  currentNodeId: '',         // Convenience-Cursor, local wins bei Merge
  createdAt: '',
  updatedAt: ''
}
```

### 4.3 Gerätelokale Präferenzen (nicht synchronisiert)

Diese Werte werden in separaten localStorage-Keys gespeichert, nie in `S`, nie im Gist.  
Das folgt dem Muster aus der Master-Referenz.

| Key-Konstante | localStorage-Key | Default | Zweck |
|---|---|---|---|
| THEME_KEY | `nabokov_theme` | `dark` | dark / light / epaper |
| FONT_PROFILE_KEY | `nabokov_font_profile` | `baskerville` | baskerville / typewriter |

Lesen: `localStorage.getItem(THEME_KEY) || 'dark'`  
Schreiben: `localStorage.setItem(THEME_KEY, value)` — **kein** `save()`, **kein** Sync-Trigger.

### 4.4 Flüchtiger UI-State (nicht persistiert, nicht synchronisiert)

Trennregel:

> Ein Feld gehört in den persistenten Projektstate, wenn sein Verlust die inhaltliche Arbeit beschädigt. Ein Feld, dessen Verlust nur eine kurze Neuorientierung erfordert (Tab nochmal anklicken, Node nochmal auswählen), ist flüchtiger UI-State.

```javascript
var UI = {
  currentTab: 'board',          // aktuell geöffneter Tab
  activeWorkflowStepId: '',     // welcher Guided Step gerade offen ist
};
```

`UI` wird nie in `S` geschrieben, nie gespeichert, nie synchronisiert.  
Es wird bei `render()` gelesen und bei Tab-/Step-Wechsel mutiert.

Sonderfall `currentNodeId`: Bleibt im `Project`, weil es über Session-Grenzen hinweg nützlich ist (App schließen, wiederkommen, am gleichen Node weitermachen). Beim Merge: **local wins**.

### 4.5 DraftNode (bestehendes Node-Modell, erweitert)

```javascript
DraftNode = {
  id: uid(),
  parentId: '',
  title: '',
  text: '',
  summary: '',
  beatId: '',                // Zuordnung zu WorkflowStep
  tags: [],                  // leichtgewichtiges Tagging statt Subplot-Grid
  status: 'draft',           // 'draft' | 'active' | 'archived'
  splitHistory: [],
  sourceId: '',              // optional: Referenz auf SourceDocument
  createdAt: '',
  updatedAt: '',
  archived: false
}
```

### 4.6 Entity

```javascript
Entity = {
  id: uid(),
  title: '',
  type: 'Figur',            // 'Figur' | 'Ort' | 'Szene' | 'Gegenstand' | 'Motiv' | 'Freie Kategorie'
  profile: '',
  cards: [],                // EntityCard[]
  tags: [],
  createdAt: '',
  updatedAt: ''
}
```

### 4.7 EntityCard

```javascript
EntityCard = {
  id: uid(),
  title: '',
  text: '',
  sourceNodeId: '',
  sourceTitle: '',
  archived: false,
  createdAt: ''
}
```

### 4.8 Relation

```javascript
Relation = {
  id: uid(),
  fromType: 'node',         // 'node' | 'entity' | 'source'
  fromId: '',
  toType: 'node',           // 'node' | 'entity' | 'source'
  toId: '',
  label: '',
  note: '',
  isInteresting: false,
  createdAt: '',
  updatedAt: ''
}
```

### 4.9 Composition

```javascript
Composition = {
  id: uid(),
  title: '',
  itemRefs: [],             // [{type:'node'|'entity-card', id:'...'}]
  note: '',
  createdAt: '',
  updatedAt: ''
}
```

### 4.10 WorkflowStep

```javascript
WorkflowStep = {
  id: '',                   // z.B. 'n1' für Nelson-Schritt 1
  title: '',
  notes: '',
  guidedQuestions: [],
  status: 'open',           // 'open' | 'in-progress' | 'done'
  decisions: [],            // StepDecision[]
  linkedNodeIds: [],
  linkedEntityIds: []
}
```

### 4.11 StepDecision

```javascript
StepDecision = {
  id: uid(),
  question: '',
  answer: '',
  variants: [],
  createdAt: ''
}
```

### 4.12 SourceDocument

```javascript
SourceDocument = {
  id: uid(),
  title: '',
  rawText: '',
  origin: 'dictation',      // 'dictation' | 'chat' | 'paste' | 'import'
  fragments: [],            // SourceFragment[]
  processed: false,
  createdAt: '',
  updatedAt: ''
}
```

### 4.13 SourceFragment

```javascript
SourceFragment = {
  id: uid(),
  text: '',
  linkedNodeId: '',
  linkedEntityId: '',
  status: 'raw'             // 'raw' | 'extracted' | 'discarded'
}
```

### 4.14 Kern vs. Modus-Zuordnung

| Objekt | Kern (beide Modi) | Nur Short-Story | Nur Prosa/Roman |
|---|---|---|---|
| Project | ✓ | — | — |
| DraftNode | ✓ | — | — |
| Entity | ✓ | — | — |
| Relation | ✓ | — | — |
| Composition | ✓ | — | — |
| WorkflowStep | ✓ (Template variiert) | Nelson-9 | Roman-Roadmap |
| StepDecision | — | ✓ (Kernfeature) | optional |
| SourceDocument | — | optional | ✓ (Kernfeature) |
| SourceFragment | — | optional | ✓ (Kernfeature) |
| premiseFields (SCOOD) | ✓ | — | — |

---

## 5. Mehrprojektmodell

### 5.1 Grundregel

Der Modus hängt am Projekt, nicht an der App. Die App hat kein globales `S.mode` mehr.

### 5.2 Struktur

- `S.projects[]` enthält alle Projekte
- `S.activeProjectId` zeigt auf das geöffnete Projekt
- Projektwechsel erfolgt über einen Project Switcher im Header
- Status-Lifecycle: `idea` → `active` → `paused` → `archived`
- Modus wird bei Projektanlage gewählt und bestimmt, welche Workflow-Templates und UI-Ansichten verfügbar sind
- Spätere Erweiterung auf `poetry` möglich

### 5.3 Projektwechsel UI

Kompaktes Dropdown im Header neben dem App-Titel. Tap öffnet Liste aller aktiven Projekte mit Modus-Badge und Status-Indikator. Unten: „Neues Projekt“ und „Alle Projekte“.

### 5.4 Projektübersicht

Eigener Tab/Screen mit Karten pro Projekt: Titel, Modus-Badge, Status, letzte Bearbeitung, Node-Count. Filterbar nach Status.

### 5.5 Helper-Funktionen

```javascript
function activeProject() {
  return S.projects.find(function(p) { return p.id === S.activeProjectId; }) || null;
}

function activeNodes()    { var p = activeProject(); return p ? p.nodes : []; }
function activeEntities() { var p = activeProject(); return p ? p.entities : []; }
function activeWorkflow() { var p = activeProject(); return p ? p.workflow : null; }
```

Alle bestehenden Render- und Datenfunktionen lesen über diese Helper statt direkt von `S`.

---

## 6. Short-Story-Modus

### 6.1 Grundidee

Kein bloßer Framework-Tab mit Beat-Liste. Stattdessen ein **Guided Mode**, in dem jeder Nelson-Schritt eine eigene Arbeitsstation ist mit Erklärung, Leitfragen, Rohnotizen-Bereich, Entscheidungsfeld, Varianten-Ablage und Verbindung zum Board.

### 6.2 Die 9 Schritte als Arbeitsstationen

| # | Schritt | Leitfragen | Felder / Artefakte |
|---|---|---|---|
| 1 | Persönliche Erfahrung | „Welche echte Erfahrung steckt dahinter?“ · „Was war der emotionale Kern?“ · „Was war das Schmerzhafte oder Ungelöste?“ | Rohnotiz, Entscheidung |
| 2 | POV-Shift | „Aus wessen Sicht ist die Geschichte am stärksten?“ · „Was passiert, wenn du die Perspektive radikal änderst?“ · „Welcher POV überrascht dich selbst?“ | Varianten + Entscheidung |
| 3 | Ticking Clock | „Welches Zeitlimit erzeugt Druck?“ · „Was passiert, wenn die Zeit abläuft?“ · „Ist der Druck extern oder intern?“ | Entscheidung |
| 4 | Symbolisches Objekt | „Welches Ding trägt die Bedeutung?“ · „Wie verändert sich das Objekt im Lauf der Geschichte?“ · „Ist es ein MacGuffin oder ein Symbol?“ | Entity-Verlinkung + Entscheidung |
| 5 | Transition | „In welchem Übergang steckt die Figur?“ · „Was ist der Point of No Return?“ · „Ist der Übergang äußerlich oder innerlich?“ | Entscheidung + Node-Verlinkung |
| 6 | Weltereignis | „In welcher Welt spielt die Geschichte?“ · „Welches reale Ereignis gibt Kontext?“ · „Wie beeinflusst die Außenwelt die Innenwelt der Figur?“ | Freitext + optional Entity |
| 7 | Binary Forces | „Welche zwei Kräfte reiben sich?“ · „Ist der Gegensatz zwischen Figuren oder innerhalb einer Figur?“ | Pole + Entity-Verlinkung |
| 8 | Physischer Raum | „Welcher Ort trägt Bedeutung?“ · „Was spiegelt der Raum über die Figur?“ · „Wie riecht/klingt/fühlt sich der Raum an?“ | Entity-Verlinkung + Entscheidung |
| 9 | Repetition & Payoff | „Was kehrt wieder?“ · „Was bekommt am Ende eine neue Bedeutung?“ · „Wie verändert sich das Wiederkehrende?“ | Rückverweise + Entscheidung |

### 6.3 Designnotiz: Abweichung von Nelson-Original bei Schritt 8 und 9

Im Nelson-Original-Video und im Freeplane-Template sind Schritt 8 und 9:
- **8: Freytags Pyramide**
- **9: Experimentiere**

In Nabokov werden Schritt 8 und 9 bewusst anders besetzt:
- **8: Physischer Raum**
- **9: Repetition & Payoff**

**Begründung dieser Abweichung:**
1. Die Buchzusammenfassung listet explizit: Schritt 8 = Physischer Raum, Schritt 9 = Repetition & Payoff.
2. Freytags Pyramide ist kein einzelner Constraint, sondern ein Makro-Strukturmodell. Sie wird in Nabokov als **optionales Struktur-Overlay** auf dem Board umgesetzt.
3. „Experimentiere“ ist eine Haltung, kein sauberer Arbeitsschritt mit Artefaktlogik.
4. Physischer Raum und Repetition & Payoff sind dagegen echte Constraints mit Leitfragen, Entscheidungen und Verlinkungen.

**Diese Zuordnung ist verbindlich für alle Patches.**

### 6.4 Vom Guided Mode zum Draft

- Jeder Schritt kann 0–n Nodes im Board erzeugen
- Aus den 9 Entscheidungen wird eine **Story Map** generiert
- Daraus kann eine **Draft-Komposition** erzeugt werden
- Der Draft ist eine `Composition`, die auf bestehende Nodes verweist

---

## 7. Prosa-/Roman-Modus

### 7.1 Arbeitszonen

**Zone 1 — Materialeingang (Sources)**
- Rohmaterial einfügen: Diktat, Chat-Material, Paste, Import
- Jedes Material wird ein `SourceDocument`
- Vorschau + manuelles Markieren relevanter Passagen
- Keine harte Vollautomatik — manuell oder AI-gestützt (HITL)

**Zone 2 — Zettelwerkstatt (Nodes + Board)**
- Aus Sources werden Nodes extrahiert
- Board-Ansicht wie bisher
- Split-Logik bleibt
- Neue Nodes können frei angelegt werden

**Zone 3 — Story-Elemente (Entities)**
- Figuren, Orte, Szenen, Gegenstände, Motive
- Karten-basiertes Anhängen von Material
- Cleanup-Workflow
- Relationen zwischen Entities und Nodes sichtbar machen

**Zone 4 — Komposition (Compositions)**
- Nodes und Entity-Cards in Reihenfolge bringen
- Vorschau des zusammengesetzten Textes
- Export als Markdown oder Copy
- Mehrere Kompositionen pro Projekt

### 7.2 Rückfluss aus geschriebenem Text ins Kartensystem

- Text-Passage im Draft markieren → als neue Node extrahieren → an Entity hängen
- Oder: Passage → neue Source → Fragmentierung → neue Nodes

---

## 8. Screen- und Tab-Architektur

### 8.1 Globale Struktur

```
[Header]
  App-Titel · Projekt-Dropdown · Hamburger (Mobile)

[Tab-Leiste]
  Variiert nach Modus des aktiven Projekts
```

### 8.2 Projektübersicht

```
Tab: Projekte
  - Karten-Grid aller Projekte
  - Filter: Status, Modus
  - „Neues Projekt“-Button
  - Pro Karte: Titel, Modus-Badge, Status, letzte Bearbeitung
```

### 8.3 Short-Story-Projektansicht

```
Tab: Guided Steps
  - Vertikale Schrittliste + aktiver Schritt
  - Erklärung, Leitfragen, Rohnotiz, Entscheidung, Varianten
  - Story Map am unteren Rand

Tab: Board
  - Gingko-Board
  - Nodes mit Step-Badges

Tab: Story-Elemente
  - Entity-Liste + Detail
  - Karten-Management, Cleanup

Tab: Komposition
  - Draft aus Nodes zusammenstellen
  - Vorschau + Export

Tab: Archiv
  - Archivierte Nodes + Entity-Cards
```

### 8.4 Prosa-Projektansicht

```
Tab: Material
  - Source-Liste + Eingabe
  - Fragmentierungs-Ansicht

Tab: Board
  - Gingko-Board

Tab: Story-Elemente
  - Entities + Cards

Tab: Komposition
  - Compositions + Vorschau

Tab: Archiv
```

### 8.5 Einstellungen

```
Tab: Einstellungen
  - Theme, Font
  - OpenAI-Token + Modell
  - Gist-Sync (Token, ID, Auto-Sync, Push/Pull/Merge)
  - Export/Import
```

---

## 9. Workflow-/Roadmap-Schicht

### 9.1 Prinzip

Der Workflow liegt **über dem Datenmodell**. Das Datenmodell kennt keine Workflow-Abhängigkeiten. Man kann jederzeit direkt ins Board springen, Entities anlegen oder Kompositionen bauen, ohne erst Schritte abzuarbeiten.

Das alte `structures`-Konzept (statische Framework-Definitionen mit `items[]`) ist vollständig im Workflow absorbiert. Es gibt keine separate `structures[]`-Liste mehr. Die Framework-Auswahl geschieht über `workflow.templateId`.

Template-Katalog:
- `nelson-9`
- `generic-9`
- `roman-roadmap`
- `frei`

### 9.2 Short-Story

Nelson-9 als WorkflowTemplate mit 9 Steps. Jeder Step hat Leitfragen, Entscheidungen, Verlinkungen. Status-Tracking: `open` → `in-progress` → `done`.

### 9.3 Prosa/Roman

Reduzierte Roadmap mit 8 Schritten. Kein Pflicht-Wizard, sondern optionale Orientierungsschicht.

### 9.4 Template-Wechsel

Wird bei Projektanlage gesetzt, kann nachträglich gewechselt werden. Wechsel überschreibt keine bestehenden Entscheidungen; neue Steps werden hinzugefügt, bestehende bleiben.

---

## 10. Migrationsplan in Phasen

### Phase 1: Projektschale einführen

**Ziel:** Mehrere Projekte in einer App, bestehende Daten erhalten.

**Konkrete Änderungen an `index_v6_fonts.html`:**
- `seedState()` erweitern: `S.projects = []`, `S.activeProjectId = ''`
- Migrationsfunktion in `load()`: Wenn `S.projects` fehlt, bestehende `nodes`, `entities`, bestehende Framework-/Workflow-Daten, `mode`, `currentNodeId` in ein neues Projekt-Objekt packen
- Helper: `activeProject()`, `activeNodes()`, `activeEntities()`, `activeWorkflow()`
- Alle Board/Entity/Framework-Renderfunktionen lesen über Helper
- Projekt-Dropdown im Header
- Neues-Projekt-Dialog: Titel + Modus
- `mergeProjects()` für Gist-Sync
- Projektübersicht als zusätzlicher Tab

**Nicht anfassen:** Board-Rendering, Entity-Panel, OpenAI-Logik, CSS.

### Phase 2: Short-Story Guided Mode

- WorkflowStep-Array pro Projekt mit Nelson-9-Template
- Neuer Tab „Guided Steps“
- Leitfragen und Entscheidungsfelder
- StepDecision-Objekte
- `beatId` an Nodes verweist auf WorkflowStep-ID
- Story Map

### Phase 3: Prosa-Modus Grundausbau

- SourceDocument + SourceFragment
- Neuer Tab „Material“
- Einfache Fragmentierungsansicht
- Composition-Tab
- Relation-Objekte

### Phase 4: Verfeinerung und Ausbau

- Versionierung pro Node
- Relationen-Ansicht
- Struktur-Overlay auf Board (Freytag)
- Statistik-Basics
- Poetry-Modus-Stub
- Turn-Back-Time für Entscheidungen und Entity-Profile

---

## 11. Technische Risiken / Konflikte

### 11.1 localStorage-Grenze

**Risiko:** Mehrere Projekte mit Source-Dokumenten → localStorage-Limit.  
**Mitigation:** `rawText` in SourceDocuments begrenzen oder warnen. Langfristig könnten Sources in ein zweites Gist-File ausgelagert werden.

### 11.2 Gist-Sync-Komplexität

**Risiko:** Merge-Logik muss pro Projekt arbeiten.

**Merge-Policy (verbindlich):**

`mergeS(localS, remoteS)`:
1. `deletedIds`: Union beider Maps
2. `projects`: `mergeProjects(local.projects, remote.projects)`
3. `activeProjectId`: local wins
4. `_lastExported`: einziger `syncTs` nach erfolgreichem Merge

`mergeProjects()`:
- Match per `project.id`
- Nur lokal → behalten
- Nur remote + nicht in `deletedIds` → hinzufügen
- Nur remote + in `deletedIds` → ignorieren
- Beidseitig → `mergeProject()`

`mergeProject(local, remote)`:
- Skalare Felder (`title`, `mode`, `premise`, `premiseFields`, `synopsis`): neuerer `updatedAt` gewinnt
- `status`: `archived` gewinnt immer
- `currentNodeId`: local wins
- `workflow.templateId`: neuerer `updatedAt` gewinnt
- `workflow.steps`: Match per `step.id`
  - `status`: `done > in-progress > open`
  - `decisions`: `mergeById(..., 'id')`
  - `linkedNodeIds`, `linkedEntityIds`: Union

Array-Felder per `mergeById()`:
- `nodes`: Match per `id`, neuerer `updatedAt` gewinnt, Tombstone-Filter
- `entities`: Match per `id`, neuerer `updatedAt` gewinnt; `entity.cards` intern ebenfalls per ID
- `relations`: Match per `id`, neuerer `updatedAt` gewinnt
- `compositions`: Match per `id`, neuerer `updatedAt` gewinnt; `itemRefs` als Block
- `sources`: Match per `id`; `rawText`: längerer Text gewinnt; `fragments`: `mergeById()`
  - `fragment.status`: `extracted > raw > discarded`

### 11.3 Single-File-Größe

**Risiko:** Datei wird mit Guided-Mode-Leitfragen und mehr UI-Code größer.  
**Mitigation:** Leitfragen als JSON-Datenblock halten, kein unnötiger HTML-String-Müll.

### 11.4 Tombstone-Kompatibilität

**Kein Konflikt.** `deletedIds` bleibt global. IDs sind per `uid()` global eindeutig.

### 11.5 AES-GCM-Kompatibilität

**Kein Konflikt.** Verschlüsselung operiert auf dem gesamten Payload.

### 11.6 Master-Referenz-Kompatibilität

| Anforderung | Status |
|---|---|
| `persistLocalOnly()` / `save()` Trennung | Erhalten |
| `_syncInProgress`-Guard | Erhalten |
| `touchObj()` bei Mutationen | Auf Projektebene anwenden |
| `saveDebounced()` | Erhalten |
| Tombstones / `deletedIds` | Erhalten |
| `THEME_KEY` / `FONT_PROFILE_KEY` getrennt | Eingehalten |
| Alle Nie/Immer-Regeln | Eingehalten |
| Single-File HTML | Eingehalten |
| Kein Framework / kein Build-Step | Eingehalten |

---

## 12. Erster nächster Build-Schritt

**Phase 1, Teil 1: Projektschale einführen in `index_v6_fonts.html`.**

Reihenfolge:
1. `seedState()` anpassen: `projects`, `activeProjectId`
2. `load()` um Auto-Migration erweitern: bestehende Daten → Default-Projekt
3. `ensureDefaults()` für neue Struktur
4. Helper-Funktionen: `activeProject()`, `activeNodes()`, `activeEntities()`, `activeWorkflow()`
5. Alle Render-Funktionen auf Helper umstellen
6. Projekt-Dropdown im Header
7. Neues-Projekt-Dialog
8. `mergeProjects()` für Gist-Sync
9. `save()` / `persistLocalOnly()` / `exportPayload()` für neue Struktur
10. Node.js-Validierung

---

## ANHANG — Nachträgliche Ergänzungen

*Neue Erkenntnisse, Patterns und Korrekturen werden hier mit Datum ergänzt.*
