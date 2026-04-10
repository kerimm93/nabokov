# AUFTRAG: Phase 1 implementieren — Projektschale für Nabokov

Du arbeitest an meiner bestehenden Single-File-App `index_v6_fonts.html`.

## Maßgebliche Referenzen
Nutze diese beiden Dokumente als verbindliche Grundlage:
1. `KERIM_APP_MASTER_REFERENZ.md` → technische Ground Truth für Single-File, localStorage, Gist-Sync, AES-GCM, State-Regeln, UI-Präferenzen, Merge-Logik, Never/Always-Regeln
2. `NABOKOV_ZIELARCHITEKTUR_v1_1.md` → Zielarchitektur der App mit Mehrprojektmodell, Short-Story-/Prosa-Modus und Phasenplan

## Ziel von Phase 1
Baue **nur** die Projektschale ein.

Das bedeutet:
- Die bisherige Ein-Projekt-App wird zu einer **Mehrprojekt-App**
- Bestehende Daten werden **verlustfrei** in ein erstes migriertes Projekt überführt
- Die bestehende App bleibt funktional
- Board, Entities, Workflow/Framework-Logik, OpenAI-Split, Theme, Gist-Sync und Grund-UI sollen **weiter funktionieren**
- Kein großer Redesign-Schritt
- Keine neuen großen Features wie Guided Steps, Sources, Relations oder Composition-UI in dieser Phase

## App-Name
Die App heißt ab jetzt **Nabokov**.

Bitte verwende diesen Namen konsistent:
- in UI-Texten
- in neuen Konstanten
- in Export-/Sync-Dateinamen
- in Dialogtiteln, wo sinnvoll

## Wichtige Korrektur gegenüber älteren Entwürfen
- `theme` und `fontProfile` dürfen **nicht** in den synchronisierten Kernstate
- Sie bleiben **gerätelokale localStorage-Präferenzen**
- Verwende getrennte Keys:
  - `THEME_KEY = 'nabokov_theme'`
  - `FONT_PROFILE_KEY = 'nabokov_font_profile'`
- Kein `S.globalConfig` für Theme/Font in Phase 1

## Weitere app-spezifische Konstanten
Verwende app-spezifische Keys im Stil der Master-Referenz, z. B.:
- `LKEY = 'nabokov_v1'`
- `GIST_TOKEN_KEY = 'nabokov_gist_token'`
- `GIST_ID_KEY = 'nabokov_gist_id'`
- `GIST_FILE = 'nabokov_data.json'`
- ggf. weitere Keys konsequent mit `nabokov_...`

## Ebenfalls wichtig
- Das alte `structures`-Konzept wird in der neuen Zielarchitektur perspektivisch vom `workflow` absorbiert
- Aber in **Phase 1** soll die bestehende Structure-/Framework-Logik **noch nicht neu erfunden** werden
- Ziel hier ist: **kompatible Projektverschachtelung**, nicht Funktionsumbau des Framework-Systems

## Konkreter Implementierungsumfang

### 1. State umbauen
Erweitere den App-State so, dass er künftig mindestens enthält:

- `S.version`
- `S.projects`
- `S.activeProjectId`
- `S.deletedIds`
- `S._lastExported`

Die bisher projektbezogenen Felder der Ein-Projekt-App sollen in ein `Project`-Objekt verschoben werden.

Ein Projekt soll in Phase 1 mindestens enthalten:
- `id`
- `title`
- `mode`
- `status`
- `premise`
- `premiseFields`
- `synopsis`
- `nodes`
- `entities`
- `compositions` (leer vorbereitbar, auch wenn UI noch fehlt)
- `relations` (leer vorbereitbar)
- `workflow`
- `sources` (leer vorbereitbar)
- `currentNodeId`
- `createdAt`
- `updatedAt`

### 2. Migrationslogik beim Load
Wenn alte Daten geladen werden und `S.projects` noch nicht existiert, dann:
- die bestehenden Ein-Projekt-Daten in **ein einziges Default-Projekt** migrieren
- Titel des migrierten Projekts: **„Mein erstes Nabokov-Projekt“**
- `mode` aus altem `S.mode` übernehmen, falls vorhanden
- bestehende `nodes`, `entities`, bestehende Framework-/Structure-Daten, aktueller Node usw. verlustfrei in dieses Projekt packen
- `S.activeProjectId` auf dieses neue Projekt setzen
- danach mit der neuen Struktur normal weiterarbeiten

Wichtig:
- Migration muss **idempotent** sein
- sie darf nicht bei jedem Start erneut auslösen
- sie darf keine bestehenden Daten duplizieren

### 3. Helper-Funktionen einführen
Führe saubere Projekt-Helper ein, damit der restliche Code möglichst wenig invasive Änderungen braucht.

Mindestens:
- `activeProject()`
- `activeNodes()`
- `activeEntities()`
- ggf. `activeWorkflow()` oder ähnliche sinnvolle Zugriffsfunktionen

Alle bestehenden Render- und Datenfunktionen sollen schrittweise über diese Helper lesen statt direkt über alte Top-Level-Felder.

### 4. Bestehende Funktionen minimalinvasiv anpassen
Passe die App so an, dass diese Bereiche projektbezogen weiterlaufen:
- Board-/Node-Rendering
- Node-Erstellung / Node-Updates / Node-Split
- Entity-Rendering / Entity-Updates
- bestehende Structure-/Framework-Nutzung
- aktueller Node
- Archiv-/Filterlogik, soweit betroffen

Nicht das Verhalten neu erfinden.
Nur so umbauen, dass dieselbe Logik jetzt innerhalb des aktiven Projekts läuft.

### 5. Projektwechsel UI einbauen
Baue eine **minimale Projektauswahl** in den Header oder in die bestehende UI ein.

Mindestens:
- Anzeige des aktiven Projekttitels
- Wechsel zwischen Projekten
- Button oder Modal zum Anlegen eines neuen Projekts

Beim Anlegen eines Projekts:
- Eingabefelder: Titel, Modus (`short-story` oder `prosa`)
- sinnvolle Defaults setzen
- passendes leeres Projekt erzeugen
- direkt aktiv schalten

Noch kein komplexes Projekt-Dashboard nötig.
Ein einfacher, funktionaler Einstieg reicht.

### 6. Gist-Sync auf `projects[]` anpassen
Passe Save/Load/Export/Import/Sync so an, dass die neue State-Struktur sauber funktioniert.

Besonders wichtig:
- die bestehende Sync-Architektur aus der Master-Referenz beibehalten
- `persistLocalOnly()` und `save()` sauber getrennt lassen
- `_syncInProgress` respektieren
- keine Tokens in `S`
- `githubHeaders()` zentral weiterverwenden
- keine Cache-Control-Header auf GitHub-GET
- nur ein gemeinsamer Sync-Timestamp pro erfolgreichem Push

### 7. Merge-Logik für Projekte
Führe eine projektbezogene Merge-Schicht ein.

Mindestanforderung:
- Projekte matchen per `project.id`
- nur lokal vorhandene Projekte bleiben erhalten
- nur remote vorhandene Projekte werden hinzugefügt, sofern nicht gelöscht
- beidseitig vorhandene Projekte werden zusammengeführt

Innerhalb eines Projekts sollen für Phase 1 mindestens diese Bereiche korrekt gemergt werden:
- `nodes`
- `entities`
- `workflow`
- ggf. bestehende Framework-/Structure-Daten
- `currentNodeId` konservativ behandeln (local wins ist okay)
- `activeProjectId` konservativ behandeln (local wins ist okay)

Wenn du intern Hilfsfunktionen wie `mergeProjects()` und `mergeProject()` einführst: gut.

### 8. Theme / Font lokal halten
Stelle sicher:
- Theme und Font werden über separate localStorage-Keys gelesen/geschrieben
- kein Gist-Sync für diese Felder
- kein Speichern dieser UI-Präferenzen in `S`
- bestehende UI-Funktionalität für Theme/Font bleibt erhalten

### 9. Nicht anfassen in Phase 1
Diese Dinge bitte **nicht** neu bauen oder groß umbauen:
- kein vollständiger Guided-Steps-Modus
- keine neue Short-Story-UI
- kein Material-/Source-Tab
- kein Relations-UI
- kein Composition-UI
- keine Version-History pro Node
- kein großes CSS-Redesign
- keine Refaktorisierung auf mehrere Dateien
- kein Framework / kein Build-Step

## Akzeptanzkriterien
Phase 1 ist erfolgreich, wenn:

1. Alte Daten beim ersten Start sauber in ein erstes Projekt migriert werden
2. Danach die App normal weiter funktioniert
3. Ich mehrere Projekte anlegen und zwischen ihnen wechseln kann
4. Nodes und Entities projektgetrennt funktionieren
5. Save/Load/Gist-Sync mit der neuen Struktur weiterläuft
6. Theme und Font weiter funktionieren, aber lokal bleiben
7. Bestehende Kernfeatures nicht kaputtgehen
8. Der Umbau minimalinvasiv bleibt

## Arbeitsstil
- arbeite defensiv
- ändere nur, was für Phase 1 nötig ist
- erhalte bestehende Funktionen so weit wie möglich
- bevorzuge kleine, klare Helper statt chaotischer Großumbauten
- wenn etwas unsicher ist, entscheide konservativ zugunsten der bestehenden Funktionalität

## Ausgabeformat
Ich will von dir:

1. **Kurze Summary**
2. **Welche Bereiche du konkret geändert hast**
3. **Den vollständigen aktualisierten Code**
4. **Kurze Liste möglicher Risiken / was ich testen soll**
