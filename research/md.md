# Novel Factory als Prozessmaschine für Roman- und Short-Story-Workflows

## 1. Executive Summary

The Novel Factory (NF) implementiert ein stark prozess-orientiertes, schrittweises Schreibmodell, das Autor:innen von der Premisse bis zur Veröffentlichung führt und dabei auf etablierten Konzepten zu Story-Elementen, Plotstruktur, Figurenentwicklung, Subplots und Redrafting aufsetzt. Die Software ist in klar abgegrenzte Bereiche gegliedert (Roadmap, Planung/Struktur, Manuskript, Supporting Data, Statistik), die zusammen ein konsistentes mentales Modell von „Projekt → Struktur → Szenen → Text → Export“ bilden.[^1][^2][^3][^4]

Kern der Prozesslogik ist die 15‑stufige Novel‑Writing‑Roadmap, die im aktuellen System sowohl im öffentlichen Roadmap‑Artikel als auch in der Roadmap-Ansicht der Software verankert ist und explizit 15 Schritte nennt. Historisch existiert daneben ein 16‑Schritte‑Modell mit einer zusätzlichen „Submissions“-Phase, das noch in älteren Blogposts, Gastartikeln und einer eigenen „Roadmap Step 16 – Submissions“-Seite sichtbar ist, aber nicht mehr im aktuellen Roadmap-Checklist UI der App reflektiert wird.[^5][^6][^7][^8][^9][^1]

Als Prozessmaschine unterstützt NF vor allem drei Übergänge: Idee → strukturierte Story (Premise & Synopses, Plot‑Manager, Goal-to-Decision‑Cycle), Struktur → Entwurf (Scene Blocking, Manuskript, Charakter-/Standortdaten) und Entwurf → überarbeitete Fassung/Publikation (Version History, Export, Roadmap‑Schritte 13–15). Für Kurzgeschichten wirkt ein Teil des Apparats (umfangreiche Weltenbau-Panels, detaillierter Subplot-Grid, Publikationsberatung) deutlich überdimensioniert, während Kernmechaniken wie Premise, kurze/erweiterte Synopsis, einfache Plotkarte und Arbeit mit Szenen gut auf einen Short‑Story‑Modus übertragbar wären.[^10][^11][^12][^13][^14][^15][^1]

Für eine eigene App legen die NF-Strukturen nahe, einen gemeinsamen Kern aus Projekt, Szenen/Beats, Entitäten (Charakter, Ort, Item), freiform Notizen, Roadmap‑/Workflow‑Schritten, Statistik und Versionen zu modellieren und darauf spezialisierte Oberflächen für Roman- vs. Short‑Story‑Flows zu setzen. NF zeigt auch, wo Grenzen eines stark linearen, formulargetriebenen Modells liegen, insbesondere für fragmentarisches, diktat- oder zettelkastenbasiertes Arbeiten, das mehr auf granulare Notizen, flexible Rekombination und konversationsbasierte Exploration setzt.[^16][^17]

## 2. Quellenbasis

Wichtige offizielle NF‑Quellen (Auswahl):

- **How to Write a Novel Step-by-Step: A Proven Roadmap** – öffentlicher Roadmap‑Artikel mit den 15 Schritten, ausführlichen Beschreibungen und Einordnung für Pantsers/Planners.[^9][^1]
- **The Roadmap (Knowledge Base)** – erklärt die Roadmap-Sektion in der Software, inklusive 15‑Themen‑Checkliste, Artikeln, Videos und Aufgaben.[^18][^5]
- **An overview of The Novel Factory** – Überblick über Sektionen: Roadmap, Planning & Structure, Manuscript, Supporting Data, Statistics.[^2][^19]
- **Navigating the software** – listet die Hauptnavigation (Roadmap, Premise and Synopses, Plot Manager, Subplot Manager, Manuscript, Characters, Locations, Items, Notes, Statistics, Recycle Bin) und User‑Menü (My Novels, Export etc.).[^4]
- **Premise and Synopses (KB)** – Panels für Premise (SCOOD‑Methode), Short Synopsis, Extended Synopsis, Pitch.[^20]
- **Plot Manager (KB)** – Index‑Karten, Plot‑Templates, Kapitel, Related Info, Verbindung zu Manuskript und Subplot‑Manager.[^10]
- **Subplot Manager (KB)** – Grid mit Szenen (Indexkarten) links und Subplot‑Spalten rechts; Unterstützung für Plot‑Templates und Character Viewpoint‑Spalten.[^21]
- **Manuscript (KB)** – Szenenliste, Editor, automatische Szenennummerierung, Szenenstatistik, Settings, Turn Back Time, Zusammenhang mit Plot‑Manager.[^13]
- **Characters, Locations, Items, Notes, Statistics (KB)** – detailreiche Panels und Kartenlogik für Figuren, Weltenbau, Objekte, freiform Notizboard, Wordcount‑ und Pace‑Statistiken.[^22][^12][^23][^13]
- **Creating a New Novel & Duplicating an Existing Novel (KB)** – My‑Novels‑Verwaltung, Mehrprojektfähigkeit, Duplikation (z. B. für Serien, neue Drafts).[^24][^25]
- **Exporting your novel and supporting data (KB)** – Export als Word mit Optionen für Szenentrenner, Kapitel-/Szenentitel, Zusatzdaten, Seitennummern, Kopfzeile.[^26]
- **Turn Back Time (version history) & Work has gone missing (KB)** – Versionierung auf Szenen-/Panel‑Ebene, automatische Backups, Recycle Bin.[^27][^14]
- **NF3 „All New“ Landing Pages** – Marketing- und Philosophie-Texte, betonen Roadmap, Templates, Prozess- und Organisationsfokus.[^28][^3][^29]

Relevante externe Analysen (Auswahl):

- ProWritingAid und Gastartikel/Blogs zum Roadmap‑Modell (z. B. 15‑Schritte‑Übersicht, Formel-Charakter).[^11][^6][^9]
- Reviews und Vergleiche, die NF als prozessgetriebene „guided workshop“-Software einordnen.[^30][^17][^15][^31][^16]
- Ältere 16‑Schritte‑Darstellungen, inkl. separatem Schritt „Submissions“.[^32][^7][^8]

## 3. Novel Factory – zugrunde liegendes Schreibmodell

NF geht von einem **stark strukturierten, schrittweisen Schreibprozess** aus, der in klar abgegrenzte Phasen gegliedert ist: Premisse → Plot‑Outline → Figurenaufbau → mehrstufige Synopsis → szenische Struktur (Scene Blocking) → Drafting → Redrafting → Submission/Publikation. Die Roadmap wird explizit als „step-by-step guide to writing a novel“ beschrieben, der neue Autor:innen vom ersten Einfall bis zur Verlagseinreichung begleitet und dabei ein destilliertes Set aus Struktur‑, Figuren‑ und Publikationswissen anbietet.[^6][^1][^5][^9]

Dieses Modell verankert eine **Top‑down‑Planung**: Der Prozess beginnt mit abstrakten Story-Elementen (Premise mit SCOOD, Plot‑Outline, Synopsis) und verdichtet sich schrittweise in Szenen und Prosa, statt spontan aus dem Schreiben heraus zu wachsen. Gleichzeitig betont NF, dass die Roadmap flexibel genutzt werden kann – einzelne Schritte dürfen übersprungen oder in anderer Reihenfolge ausgeführt werden, und Pantsers können sie nachträglich zum Analysieren und Nachschärfen einer bestehenden Rohfassung nutzen.[^3][^1][^20][^9]

NF nimmt an, dass **Romane komplexe, multi-dimensionale Systeme** sind, in denen Plotstruktur, Figurenentwicklung, Schauplätze, Subplots und Themen bewusst designt und verzahnt werden sollten, um Plotlöcher, pacing‑Probleme und flache Figuren zu vermeiden. Hierfür bietet die Software spezialisierte Oberflächen: Plot‑Manager für Makrostruktur, Subplot‑Manager für Multi-Thread‑Plots, tief strukturierte Charakter‑ und Location‑Panels und Statistik‑Views für Wordcount- und Pace-Kontrolle.[^12][^15][^1][^2][^22][^10]

### Lineares vs. hybrides Arbeiten

Obwohl die Roadmap formal linear ist (Schritte 1–15), positioniert NF sie als **empfohlene Route, nicht als starre Pipeline**: Autor:innen sollen ihren eigenen Weg finden, gegebenenfalls Schritte auslassen oder in andere Reihenfolgen bringen. Zugleich ist die gesamte UI so gestaltet, dass ein linearer Weg naheliegt: Roadmap‑Checkliste mit Häkchen, zugehörige Aufgaben, und direkte Sprünge in die passenden Sektionen (z. B. Premise‑Panel, Plot‑Manager, Characters).[^1][^5][^4][^18]

Das Modell unterstützt damit vor allem **strukturorientierte Autor:innen** (Planners, Outliner), die einen planungsintensiven Vorlauf vor dem eigentlichen Schreiben bevorzugen, und **Anfänger:innen**, die „Hand‑holding“ und vorgefertigte Templates suchen. Für Discovery Writer*innen („Pantsers“) ist explizit vorgesehen, dass sie entweder nur ausgewählte Roadmap‑Schritte nutzen oder das Tool vor allem zur nachträglichen Strukturierung und Fehlersuche einsetzen.[^31][^30][^3][^1]

### Implizite Zielgruppe und Werktyp

Die gesamte Struktur – 90k‑Wort‑Zielwerte, detaillierte Subplot‑Grids, tiefes Weltenbau‑Schema, eigene Schritte für Locations und Subplots, Publikationsberatung – ist klar auf **vollwertige Romane** (eher Genre‑Fiktion) ausgerichtet. Kurzgeschichten werden zwar erwähnt, aber nicht im Zentrum der Roadmap; NF‑Reviews betonen NF dennoch als hilfreich für „short story“‑Schreiben, vor allem wegen Figuren‑Builder, Plot‑Tools und Roadmap als Lernwerkzeug, nicht wegen der vollständigen Apparatur.[^17][^15][^12][^1]

## 4. Detaillierte Analyse der Roadmap

### 4.1 Vollständige Roadmap-Schritte (aktuelles 15‑Schritte‑Modell)

Aus dem Hauptartikel und der 15‑Schritte‑Videoübersicht ergeben sich folgende Schritte:[^9][^1]

1. Write a Premise
2. Develop a Plot Outline
3. Complete Character Introductions
4. Write a Short Synopsis
5. Expand that into an extended Synopsis
6. Establish a Goal to Decision Cycle
7. Carry out detailed Character Development
8. Scene Blocking / Do your Scene Blocking
9. Write your First Draft
10. Research your Locations
11. Develop subplots / Subplots
12. Write Character Viewpoints
13. Redraft and Edit / Redrafting and editing
14. Final Polishing and get Feedback
15. Get published / Getting Published

Die Roadmap‑KB spricht von einer 15‑Themen‑Checkliste in der Roadmap‑Sektion der Software, was diese Struktur im UI bestätigt.[^5]

### 4.2 15 vs. 16 Schritte – historische Abweichungen

Ältere Darstellungen (z. B. ein Ink‑and‑Quills‑Gastpost) listen 15 Schritte mit anderer Reihenfolge und Benennung (inkl. „Location Development“, „Advanced Plotting“, „Theme and Variation“, „Second Draft“, „Final Draft“). Andere externe Quellen (Wattpad‑How‑to, Blogartikel) sprechen von „16 steps“ und führen explizit eine zusätzliche Phase „Submissions“ an; NF selbst hostet eine Seite „How to Write a Novel Step Sixteen: Submissions“, die detaillierte Hinweise zum Agenten‑/Verlags‑Submissionsprozess gibt.[^33][^7][^8][^6][^32]

Die aktuelle offizielle Roadmap (Hauptartikel, Video‑Overview, Roadmap‑Checklist in der App) umfasst jedoch nur 15 Schritte und behandelt „Getting Published“ inklusive Agenten/Publisher‑Abwägungen; die Step‑16‑Submissions‑Seite ist eher ein Relikt bzw. Ergänzungsartikel und nicht als eigener Roadmap‑Eintrag in der aktuellen Software ausgezeichnet.[^1][^5][^9]

### 4.3 Roadmap-Tabelle

Die folgende Tabelle verdichtet die Roadmap im Hinblick auf Zweck, Artefakte, Software-Sektion und Übertragbarkeit (Einschätzung basierend auf offizieller Beschreibung und Funktionszuordnung):[^22][^13][^20][^10][^1]

| Schritt | Zweck (inhaltlich) | Erzeugte Artefakte | Unterstützende Bereiche in NF | Nutzen für Roman | Nutzen für Kurzgeschichte | Übertragbarkeit auf deine App |
|--------|---------------------|---------------------|-------------------------------|-------------------|---------------------------|--------------------------------|
| 1. Premise | Story‑Kern testen: Figur, Situation, Ziel, Gegenspieler, Katastrophe zu einer tragfähigen Storyidee verdichten (SCOOD). | Eine einzeilige Premise mit SCOOD‑Feldern. | Roadmap‑Artikel „Premise“, Premise‑Panel in „Premise and Synopses“. | Hoch: verhindert schwache Kernideen, gibt Nordstern für langen Plot. | Hoch: komprimierte Premise ist auch für Shorts zentral. | Direkt übernehmbar als Premise‑Editor (ggf. SCOOD optional), global für beide Modi. |
| 2. Plot Outline | Grobe Makrostruktur entwickeln (Setup, Inciting Incident, Midpoint, Climax etc.). | Textliche Plot‑Outline, ggf. listig; initiale Indexkarten aus Plot‑Template. | Roadmap‑Artikel, Plot‑Manager mit Genre‑Templates. | Sehr hoch: zentrale Strukturierung des Romans. | Mittel: für einfache Kurzgeschichten evtl. nur 3‑Akt‑Mini‑Outline nötig. | Übertragbar als Plot‑Beats‑Ebene (Timeline / Board); Short‑Story‑Modus kann eine vereinfachte Outline‑Schicht anbieten. |
| 3. Character Introductions | Kernfiguren grob anlegen (Rolle, Motivation, Konflikte). | Basiseinträge für Hauptfiguren (Karten, kurze Beschreibungen). | Roadmap‑Artikel, Characters‑Sektion (Basic Info, kurze Beschreibung). | Sehr hoch: frühe Klarheit über Protagonist:in & Gegenspieler. | Hoch: Shorts profitieren von klaren, fokussierten Figuren. | Übertragbar als „Lightweight Character Seeds“, getrennt von tiefer Charakterarbeit; in beiden Modi. |
| 4. Short Synopsis | Einseitige Übersicht über Plotkern ohne Subplots. | 1‑seitige Synopsis (ca. 500 Wörter). | Short‑Synopsis‑Panel in „Premise and Synopses“. | Hoch: Check auf strukturelle Stimmigkeit, spätere Agenten‑Synopsis. | Mittel: für kurze Stories oft eher Logline + Outline ausreichend. | Übernehmbar als optionaler „One‑Pager“; für Short‑Story‑Modus evtl. optional, für Romanmodus stark empfohlen. |
| 5. Extended Synopsis | Plot und Subplots ausformulieren, Details ergänzen. | Mehrseitige Extended Synopsis. | Extended‑Synopsis‑Panel. | Hoch: bietet Brücke zwischen Outline und Szenenliste. | Niedrig–mittel: kann für komplexere Novellen sinnvoll sein, meist Overkill für sehr kurze Texte. | In Romanmodus als „Outline‑Prosaebene“ sinnvoll; im Short‑Modus optional oder stark gekürzt. |
| 6. Goal to Decision Cycle | Szenenlogik über Ziel → Konflikt → Disaster → Reaktion → Dilemma → Entscheidung kontrollieren. | GtD‑Angaben pro Szene/Beat (Felder im Related‑Info‑Panel). | Roadmap‑Artikel, Related Info in Plot‑Manager/Manuscript (Goal‑to‑Decision‑Feld). | Sehr hoch bei plotgetriebenen Romanen; hilft Pacing und innerer Logik. | Mittel: nützlich für dramaturgisch dichte Kurzgeschichten, aber nicht immer nötig. | Übertragbar als optionales „Scene logic schema“ mit Feldern; eher für Romanmodus standard, im Short‑Modus als Analyse‑Werkzeug. |
| 7. Detailed Character Development | Tiefe, vielschichtige Figuren (Backstory, Voice, Motivationen, Flaws, Beziehungen). | Ausgefüllte Panels (Backstory, Voice, Personality etc.). | Characters‑Sektion mit umfangreichen Panels und Fragebögen. | Sehr hoch: Kern für Figuren‑getriebene Romane. | Variabel: für charakterschwere Shorts nützlich, ansonsten Overkill. | Übertragbar als modulare Charakter‑Profile mit optionalen Panels – in Short‑Modus deutlich reduzierter Standardumfang. |
| 8. Scene Blocking | Szenen grob planen: Was passiert, welche Beats, evtl. Dialog‑Snippets. | Szenenliste / Indexkarten mit Kurzbeschreibungen. | Plot‑Manager (Index Cards), Manuscript‑Szenenliste (automatisch verknüpft). | Sehr hoch: reduziert Plotlöcher, erleichtert Drafting. | Mittel: für längere Novellen hilfreich, für sehr kurze Stories genügt oft direkte Draftarbeit. | Kernmechanik: allgemeines „Scene/Beat‑Board“ im gemeinsamen Kern, für beide Modi. |
| 9. First Draft | Volltext der Geschichte schreiben, Fokus auf Durchlauf statt Perfektion. | Manuskript‑Text in Szenenstruktur. | Manuscript‑Sektion (Editor, Szene‑Statistik, Autosave, Version History). | Offensichtlich zentral. | Zentral für jede Form von Prosa. | Vollständig übernehmbar, allerdings mit Option auf alternative Eingaben (Diktat, Chat‑Drafting, Fragmentmodus). |
| 10. Locations | Schauplätze ausgestalten, Atmosphäre, Sinneseindrücke und Weltenbau. | Location‑Karten mit detaillierten Panels (Klima, Gesellschaft, Magie etc.). | Locations‑Sektion (Gallery, umfangreiche Weltenbau‑Panels). | Sehr hoch für Fantasy/SF/Historiensettings, moderat für realistische Romane. | Gering–mittel: meist nur wenige, skizzierte Orte nötig; Weltenbau‑Panels eher überdimensioniert. | Übertragbar als generische „Setting“‑Objekte, aber in einem Short‑Story‑Modus stark reduziert; Weltenbau‑Superstruktur optional/erweiterbar. |
| 11. Subplots | Subplots, Themen, Figurenbögen gegen Hauptplot grid‑basiert ausbalancieren. | Subplot‑Events im Grid, farbcodierte Spalten. | Subplot‑Manager (Indexkarten links, Subplot‑Spalten rechts). | Sehr hoch bei komplexen Romanen mit mehreren Plotsträngen. | Gering: die meisten Kurzgeschichten haben 0–1 Subplots. | Übertragbar als generischer „Thread/Tag“‑Grid, aber im Short‑Modus nur als optionales Feature; Romanmodus: Kernwerkzeug. |
| 12. Character Viewpoints | Story aus Sicht wichtiger Nebenfiguren nacherzählen, um Tiefe und Kohärenz zu prüfen. | Character Viewpoint‑Synopsen (Text pro Szene pro Figur). | Charakter‑Detailpanel „Character Viewpoint Synopsis“, referenziert Indexkarten. | Hoch für epische/multi‑POV‑Romane, geringer für Simple‑POV‑Texte. | Gering: für typische Kurzgeschichten eher Overkill. | Übertragbar als Analyse‑Werkzeug im Romanmodus; im Short‑Modus selten relevant. |
| 13. Redraft and Edit | Struktur‑, Szenen‑ und Satzebene überarbeiten, Szenen hinzufügen oder löschen. | Überarbeitete Manuskriptfassungen, ggf. Szenen‑Reorganisation. | Manuscript (Turn Back Time, Szenenlöschung), Plot‑/Subplot‑Manager für Umbau. | Sehr hoch. | Hoch: Editing ist auch für Kurztexte kritisch, aber weniger komplex. | Kernmechanik: Versionierung, Vergleichsansichten, Alternativfassungen pro Szene/Segment; in beiden Modi, aber mit unterschiedlicher Tiefe. |
| 14. Final Polishing and Feedback | Letzte stilistische Feinschliffe und externe Rückmeldung einholen. | Finaler Text, Feedback‑Notizen. | Kein eigenes Modul; Roadmap‑Artikel, ggf. Notes‑Sektion zur Feedback-Ablage. | Hoch. | Hoch. | Übertragbar als Feedback‑/Review‑Ebene (Kommentare, Notiz‑Verknüpfung) unabhängig vom Modus. |
| 15. Get Published | Publikationsweg wählen (traditionell vs. Self‑Publishing), Submission‑Materialien vorbereiten. | Exportiertes Manuskript (Word/PDF), Anschreiben, Pitch, Synopsis. | Export‑Funktion, Premise & Synopses (Pitch, Short/Extended Synopsis), ggf. Notes. | Hoch für Romane, die in den Markt sollen. | Niedrig–mittel: je nach Veröffentlichungsambition der Kurztexte. | Übertragbar als Export‑ und „Submission Package“-Feature; für Shorts evtl. simplere Exportszenarien (z. B. Magazin‑Guidelines). |

## 5. Analyse der Kernbereiche / Features

### 5.1 Roadmap

**Zweck:** Die Roadmap ist didaktischer Kern und Prozessmotor: Sie bietet Artikel, Videos und Aufgaben zu 15 Themen, verknüpft diese mit konkreten Tasks in den jeweiligen Sektionen und erlaubt Fortschritts‑Tracking per Checkliste. NF positioniert sie explizit als Lernpfad für Einsteiger, gleichzeitig als strukturierende Ergänzung für fortgeschrittene Autor:innen.[^30][^18][^5][^1]

**Typische Eingaben/Ausgaben:** Eingaben sind das Abarbeiten der Aufgaben (Premise schreiben, Figuren anlegen, Szenen blocken usw.); Ausgaben sind abgehakte Checkboxes und die in anderen Sektionen entstandenen Artefakte (Premise, Outlines, Szenen, Figurenprofile).[^13][^20][^5]

**Arbeitsweise/UI:** Linke Seitenleiste mit Inhaltsliste (15 Themen mit Checkbox), zentraler Artikeltext, rechts Video und Task‑Block mit eigener „Completed“-Checkbox, die mit der Inhaltsliste synchronisiert ist. Roadmap fungiert damit als „Wizard“ über die sonst eher generischen Tools.[^18][^5]

**Zusammenspiel:** Roadmap‑Tasks verweisen explizit auf Premise‑Panel, Plot‑Manager, Characters, Locations, Subplot‑Manager, Manuskript etc.; die eigentliche Dateneingabe passiert dort, Roadmap ist Prozessschicht darüber.[^20][^1]

**Relevanz für deine App:** Roadmap ist weniger ein Feature als eine **Workflow-Orchestrierungsschicht** – übertragbar als konfigurierbare Workflows/Playbooks pro Modus (z. B. Short‑Story‑Roadmap mit 6–8 Schritten, Roman‑Roadmap mit 12–15 Schritten). Wichtig: Schritte mit echten Artefakt‑Targets verknüpfen, nicht nur „Checklisten“.

### 5.2 Premise / Synopses

**Zweck:** „Premise and Synopses“ bündelt alle hochformatigen Story‑Abstraktionen: Premise (SCOOD), Short Synopsis, Extended Synopsis und Pitch. Dies ist der Knotenpunkt zwischen Idee, Plan und Submission‑Material.[^20]

**Typische Eingaben/Ausgaben:** Eingaben sind freier Text in den Panels (Premise‑Felder, einseitige Kurz‑Synopsis, längere Extended‑Synopsis, Pitch); Ausgaben sind diese Texte selbst und ggf. Versionen über Turn Back Time im Short‑Synopsis‑Panel.[^14][^20]

**Arbeitsweise/UI:** Panel‑System: Hover → Edit‑Button → Popup mit Feldern → Save & Close; in View‑Modus zeigt das Panel nur befüllte Fragen/Abschnitte, um die UI schlank zu halten. Short Synopsis unterstützt Turn Back Time, sodass frühere Fassungen reaktivierbar sind.[^14][^20]

**Zusammenspiel:** Premise und Synopses bilden den semantischen „Nordstern“ für Plot‑Manager, Subplot‑Manager und Manuskript; Roadmap‑Schritte 1, 4, 5 und 15 verweisen direkt auf diese Panels. Export kann Pitch/Synopsis als Teil des Submission‑Packages nutzen.[^26][^1][^20]

**Relevanz:** Für deine App sehr übertragbar als **Story‑Abstraktionsschicht**. Für Kurzgeschichten ließen sich Premise + Pitch + optional kurze Synopsis anbieten; Extended‑Synopsis könnte Roman‑Modus vorbehalten oder als erweiterter Modus konfigurierbar sein.

### 5.3 Plot Manager

**Zweck:** Plot Manager ist ein **Makro-Strukturboard**: Indexkarten‑Corkboard zur Planung des Plots und zum schnellen Re‑Arrangieren von Szenen. Er dient sowohl zum initialen Plotten (mit Templates) als auch zur Reorganisation bestehender Drafts.[^10]

**Typische Eingaben/Ausgaben:** Eingaben sind Indexkarten (Titel, Beschreibung), Kapitelgruppen, Auswahl aus Plot‑Templates, Verknüpfung von Related Info (Figuren, Orte, Items, Subplots). Ausgaben sind die Kartenstruktur und die automatisch dazugehörigen Szenen im Manuskript.[^13][^10]

**Arbeitsweise/UI:** Corkboard mit drag&drop‑fähigen Karten, Kontexmenü (Edit/Delete/Open Scene), Toolbar mit Buttons für „Add Index Card“, „Add Plot Template“, „Add Chapter“, Background‑Theme‑Wechsel und Related‑Info‑Filter. Jede Karte entspricht einem Manuskript‑Scene‑Objekt; Löschungen propagieren in beide Richtungen.[^10][^13]

**Zusammenspiel:** Plot‑Manager ist der strukturelle Zwilling des Manuskripts; Subplot‑Manager zeigt dieselben Indexkarten in einer Spalte, Character‑Viewpoint‑Synopsen nutzen die Kartenliste als Referenz.[^21][^22][^10]

**Relevanz:** Ein **Scene/Beat‑Board** mit 1:1‑Verknüpfung zur Textebene ist auch für deine App ein geeigneter Kernbaustein. Für Kurzgeschichten erlaubt derselbe Mechanismus, wenige Szenen/Beats zu strukturieren; für Romane wird er zum zentralen Architekturtool. Wichtig ist die generische Modellierung (Karte <-> Textblock), damit auch diktierte oder fragmentarische Texte daran andocken können.

### 5.4 Subplot Manager

**Zweck:** Subplot‑Manager ist ein **Cross‑Reference‑Grid** für mehrere Handlungsstränge, Themen, Figurenbögen etc., die über Szenen hinweg verfolgt werden. Er adressiert das Problem, in langen Romanen den Überblick über parallele Threads zu behalten.[^21]

**Typische Eingaben/Ausgaben:** Eingaben sind Subplot‑Spalten (manuell oder aus Plot‑Templates), Subplot‑Events (Karten in Spalten), Spalten für Character Viewpoint‑Synopsen. Ausgaben sind die Matrix „Szenen x Subplots“ und automatische Verknüpfungen der Subplot‑Events mit Szenen (werden in Related Info der Szene angezeigt).[^21][^10]

**Arbeitsweise/UI:** Linke Spalte zeigt alle Indexkarten (Szenen), rechts Subplot‑Spalten; Toolbar zum Hinzufügen von Plot‑Template‑Spalten, neuen Subplots oder Viewpoint‑Spalten und Layout‑Optionen (Kartengröße, Anzeige, Zeilen/Spalten‑Wechsel). Plot‑Templates duplizieren den Main‑Plot sowohl als Indexkarten als auch als Subplot‑Spalte, um Originalbeats als Referenz zu erhalten.[^21]

**Zusammenspiel:** Subplot‑Events erscheinen automatisch im Related Info der entsprechenden Szene; Verschiebungen müssen im Subplot‑Manager erfolgen. Character Viewpoint‑Spalten verknüpfen Plotstruktur mit Figurensicht.[^10][^21]

**Relevanz:** Für Romanmodus ein starkes Strukturwerkzeug; für Kurzgeschichten meist überdimensioniert. Abstrakt handelt es sich um ein **multidimensionales Tagging/Threading** von Szenen – übertragbar, wenn man Threads generischer denkt (Themen, Motive, Timeline‑Segmente) und UI ggf. vereinfacht.

### 5.5 Manuscript

**Zweck:** Manuscript ist der zentrale **Schreibworkspace**: Szenenbasierter Editor mit Szenenliste, Statistiken, Formatoptionen und Version History.[^13]

**Typische Eingaben/Ausgaben:** Eingaben sind Szenentexte, Settings (Fonts, Line Spacing), Szenenverwaltung (neu, löschen, umsortieren); Ausgaben sind der Volltext, Szenenstatistik (Wordcounts, kumulative Counts) und Versionen via Turn Back Time.[^14][^13]

**Arbeitsweise/UI:** Linke Szenenliste mit automatischer Nummerierung, mittlerer Editorbereich, Toolbar mit Save, +Scene, Scene Statistics, Settings, Delete (Bin) und Version‑History‑Icon. Szenen sind einzelne Objekte; neue Szenen erzeugen automatisch eine neue Indexkarte im Plot‑Manager und umgekehrt.[^13][^10]

**Zusammenspiel:** Manuskript ist eng mit Plot‑Manager (Indexkarten) und Subplot‑Manager (Subplot‑Events) verzahnt; Related Info‑Sidebar ermöglicht Link zu Figuren, Orten, Items, Notes und Subplot‑Events aus der Szene heraus. Statistikmodul liest Wordcounts aus dem Manuskript.[^12][^10][^13]

**Relevanz:** Dein Kern‑Textlayer kann sich an diesem Szenen‑Modell orientieren, sollte aber zusätzlich **Fragment‑ und Dictation‑Workflows** unterstützen (z. B. Zwischenschicht aus Notiz‑Fragments, die später Szenen zugeordnet werden). Wichtig ist, Turn‑Back‑Time/Versionen nicht nur pro Szene, sondern ggf. pro beliebigem Textblock verfügbar zu machen.

### 5.6 Characters

**Zweck:** Characters‑Sektion ist ein **Charakter‑Datenbank und Entwicklungswerkzeug** mit umfangreichen Panels für Biografie, Voice, Beziehungen, Werte etc.[^22]

**Typische Eingaben/Ausgaben:** Eingaben sind Charakterkarten (Name, Bild, Kurzbeschreibung), detaillierte Panel‑Einträge (Backstory, Voice, Personality, Friends and Family etc.), Character Viewpoint‑Synopsen. Ausgaben sind strukturierte Charakterprofile mit verlinkter Related Info (Szenen, Orte, Items, Notes).[^22]

**Arbeitsweise/UI:** Übersicht zeigt Karten (drag&drop), Liste links, Detailansicht mit Panels und Gallery; Panels mit Hover‑Edit‑Button und „nur befüllte Felder anzeigen“ im View‑Modus. Character Viewpoint‑Synopsis bietet zwei‑spaltige Ansicht: links Szenen‑Indexkarten, rechts Textfelder pro Szene.[^22]

**Zusammenspiel:** Figuren können mit Szenen, Orten, Items und Notes verlinkt werden; sie tauchen in Related Info in Plot‑Manager, Manuscript und Locations auf. Viewpoint‑Synopsen hängen an der Szenenliste (Indexkarten) und sind sensibel für Szenenlöschungen.[^10][^22]

**Relevanz:** Für Romanmodus stark; für Short‑Story‑Modus sollte dieselbe Entität existieren, aber mit leichterem UI (weniger Panels, mehr Freiform). NF zeigt, wie man Panels mit hohem Umfang über **adaptive Anzeige (nur ausgefüllte Felder)** UI‑seitig erträglich halten kann.

### 5.7 Locations

**Zweck:** Locations ist eine **Weltenbau‑/Settings‑Datenbank** mit tiefen Prompts zu Klima, Politik, Wirtschaft, Magie etc. Ziel ist, Settings nicht nur als Kulisse, sondern als aktive Story‑Komponente zu gestalten.[^23][^13]

**Typische Eingaben/Ausgaben:** Eingaben sind Location‑Karten (Bild, Beschreibung), detailreiche Panels (Senses, Governance, Religion, Magic Users etc.), Bildergalerien; Ausgaben sind reich ausformulierte Setting‑Profile.[^13]

**Arbeitsweise/UI:** Karten‑Übersicht, Liste, Details mit zahlreichen Panels und Gallery; Panels funktionieren wie bei Characters (Hover‑Edit, nur ausgefüllte Felder zeigen, Panel‑Visibility konfigurierbar).

---

## References

1. [How to Write a Novel Step-by-Step: A Proven Roadmap](https://www.novel-software.com/how-to-write-a-novel/) - The Roadmap is a step-by-step guide to writing a novel, which takes you from initial idea all the wa...

2. [An overview of The Novel Factory – Novel Factory](https://www.novel-software.com/knowledge-base/an-overview-of-the-sections/) - The Novel Factory's key features and functions are split into sections, which are loosely grouped as...

3. [Novel Factory just got even better at helping you finish your novel](https://nf3.novel-factory.com/all-new?fpr=h-23)

4. [Navigating the software – Novel Factory](https://www.novel-software.com/knowledge-base/navigating-the-software/) - There are two main ways to navigate the Novel Factory software:

5. [The Roadmap - The Novel Factory](https://www.novel-software.com/knowledge-base/the-roadmap/) - The Roadmap is a step-by-step guide to writing a novel. It has four components: The checklist; The a...

6. [The Novel Writing Roadmap: A Guest Post by Katja Kaine - Ink and Quills](https://inkandquills.com/2016/04/14/novel-writing-roadmap/) - The following is a guest post from Katja Kaine, writer, blogger, and creator of The Novel Factory wr...

7. [From Planning to Publication: Novel Factory’s 16 Step Writing Method](https://tooleybook.com/blog/from-planning-to-publication-novel-factorys-16-step-writing-method/)

8. [Roadmap Step 16 - Submissions – Novel Factory](https://www.novel-software.com/submissions/) - Wow, you're ready to submit - exciting times!

9. [How to Write a Novel in 15 steps - From Idea to Publication](https://www.youtube.com/watch?v=whEV-fucTnw) - If you would like to write a novel, but you’re not sure where to start, then you’ve come to the righ...

10. [The Plot Manager – Novel Factory](https://www.novel-software.com/knowledge-base/plot-manager/) - The Plot Manager works a bit like a corkboard or whiteboard; it's a space where you can add index ca...

11. [The Roadmap to Novel Writing Success! - ProWritingAid](https://prowritingaid.com/art/285/A-Novel-Writing-Formula.aspx) - This will include full name, age, appearance, summary of role and motivation. Character Traits in Th...

12. [Statistics - The Novel Factory](https://www.novel-software.com/knowledge-base/statistics/) - The statistics section has been designed to give you useful data relating to your novel, and help ke...

13. [Manuscript - The Novel Factory](https://www.novel-software.com/knowledge-base/manuscript/) - The Manuscript section is the most important part of the software, as this is where you write your n...

14. [Turn Back Time (version history) - The Novel Factory](https://www.novel-software.com/knowledge-base/turn-back-time-version-history-2/) - The Novel Factory includes a 'Turn Back Time' or 'Version History' feature. This automatically saves...

15. [Novel Factory Review: Great for Storytelling Beginners!](https://neilchasefilm.com/novel-factory-review/) - Is Novel Factory the right creative writing software program for you? Find out in this review, inclu...

16. [The Novel Factory Review: Best Writing Software for 2027](https://www.automateed.com/the-novel-factory) - Key features include story templates, a character builder, scene cards, plot management tools, progr...

17. [Plottr Versus Novel Factory | Science Fiction Author](https://boldly.blue/plottr-versus-novel-factory/) - It's the kind of tool where you can take an existing draft and pin “editing notes” to the structure—...

18. [The Roadmap | The Novel Factory](https://www.youtube.com/watch?v=g-3u07Qgh2o)

19. [Sections of The Novel Factory Archives – Novel Factory](https://www.novel-software.com/article-categories/sections-of-the-novel-factory/)

20. [Premise and Synopses - The Novel Factory](https://www.novel-software.com/knowledge-base/premise-and-synopses/) - The Premise and Synopses section is where you pin down the heart of your novel ... Try The Novel Fac...

21. [The Subplot Manager - The Novel Factory](https://www.novel-software.com/knowledge-base/subplot-manager/) - Try The Novel Factory free for 30 days — no payment details required. ... The Subplot Manager is des...

22. [Characters - The Novel Factory](https://www.novel-software.com/knowledge-base/characters/) - The Characters section is where you can create and keep track of your characters, using visuals and ...

23. [Notes - The Novel Factory](https://www.novel-software.com/knowledge-base/notes/) - The Notes section is where you can keep research and any other information that doesn't fit into the...

24. [Creating a new novel - The Novel Factory](https://www.novel-software.com/knowledge-base/creating-a-new-novel/) - To do this, navigate to the 'My Novels' section and then click the 'copy' icon above the novel you w...

25. [Duplicating an existing novel - The Novel Factory](https://www.novel-software.com/knowledge-base/duplicating-an-existing-novel/) - To duplicate an existing novel, navigate to the 'My Novels' section and then click the 'copy' icon a...

26. [Exporting your novel and supporting data – Novel Factory](https://www.novel-software.com/knowledge-base/exporting-your-novel-and-supporting-data/) - To export your novel and all the supporting data, go to the user menu in the top right-hand corner a...

27. [Work has gone missing – Novel Factory](https://www.novel-software.com/knowledge-base/work-gone-missing/) - Keeping our users' data safe is our utmost priority, and we go to great lengths to make sure everyth...

28. [Novel Factory 3.0 — All New!](https://www.novel-software.com/all-new/) - Novel Factory just got even better at helping you finish your novel!

29. [Novel Factory just got even better at helping you finish your ...](https://nf3.novel-factory.com/all-new?fpr=105576)

30. [The Novel Factory Review | The Writer's Cookbook](https://www.writerscookbook.com/the-novel-factory-review/) - The Novel Factory is an in-depth writing software that tracks every stage of the writing and publica...

31. [Novel Factory Review - The Ultimate Software for Writers?](https://selfpublishing.com/novel-factory-review/) - In this Novel Factory review, we'll look at who it's for, what it is, how it works, how much it cost...

32. [16 Steps to a Novel - CloakedLoup - Wattpad](https://www.wattpad.com/story/164154795-16-steps-to-a-novel) - How to plan, write, and complete your novel in 16 steps. (By the Novel Factory) ... adviceguidestepb...

33. [Page 3 of 9 - tips and tools to tell your story - Ink and Quills](https://inkandquills.com/page/3/) - tips and tools to tell your story

