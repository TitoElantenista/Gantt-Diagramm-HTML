# 📊 Gantt-Diagramm HTML Editor

Ein interaktiver, eigenständiger HTML-Projektplaner zur Erstellung, Bearbeitung und Visualisierung von Gantt-Diagrammen mit Arbeitstagen und bundesweiten Feiertagen.

## 📋 Übersicht

**Gantt Editor** ist eine vollständig eigenständige Webanwendung (eine einzige HTML-Datei), die es ermöglicht, Gantt-Diagramme interaktiv zu erstellen, zu bearbeiten und zu visualisieren, ohne Python oder einen Backend-Server zu benötigen.

Das Tool berechnet automatisch Arbeitstage (Montag-Freitag) unter Berücksichtigung der bundesweiten deutschen Feiertage.

## ✨ Hauptfunktionen

### 🎯 Aufgabenverwaltung
- **Aufgaben und Meilensteine erstellen** mit visuellem Formular
- **Aufgaben bearbeiten** durch Klicken
- **Aufgaben löschen** einzeln
- **Organisation** nach Gruppen/Phasen
- **Start- und Enddaten** mit automatischer Berechnung
- **Arbeitstage-Berechnung** (Mo-Fr, ohne bundesweite Feiertage)
- **Geplante Dauer** (optional)
- **Tonnage** (optional, für Bauprojekte)
- **Individueller Text** auf Balken
- **Drag & Drop** zum Neuordnen von Aufgaben

### 📈 Visualisierung
- **Interaktives Gantt-Diagramm** mit Plotly
- **Unabhängiger horizontaler und vertikaler Zoom**
- **Zeitraumregler** für zeitliche Navigation
- **Automatische Farben** nach Gruppen
- **Informative Tooltips** mit allen Aufgabendetails
- **Responsive Design** für verschiedene Bildschirmgrößen

### 📊 Projektanalyse
- **Automatische Berechnung** der reinen Arbeitszeit
- **Erkennung von Unterbrechungen** zwischen Aufgaben
- **Gesamtprojektdauer** mit Arbeitstagen und Wochen
- **Statistiken nach Gruppen** mit Auslastung
- **Detaillierte Unterbrechungsanalyse**

### 💾 Datenverwaltung
- **Konfiguration als JSON speichern**
- **Konfiguration aus JSON laden**
- **Projekte exportieren/importieren**
- **PDF-Export** des Gantt-Diagramms

### 🎨 Benutzeroberfläche
- **Modernes, responsives Design**
- **Registerkartenbasierte Navigation**: Aufgaben, Analyse, Konfiguration
- **Aufgabenliste** mit Vorschau
- **Suchfunktion** für Aufgaben
- **Leere Zustände** mit hilfreichen Informationen
- **Formularvalidierung**

### ⌨️ Tastaturkürzel
- **Strg+S** - JSON speichern
- **Strg+O** - JSON laden
- **Strg+N** - Neue Aufgabe
- **Strg+G** - Diagramm generieren
- **Esc** - Modal schließen

## 🚀 Verwendung

### Methode 1: Direkt öffnen
```bash
# Zum Ordner navigieren
cd Gantt-Diagramm-HTML

# Im Browser öffnen
xdg-open gantt-editor.html   # Linux
open gantt-editor.html        # macOS
start gantt-editor.html       # Windows
```

### Methode 2: Lokaler Server (optional)
```bash
# Mit Python 3
python3 -m http.server 8000

# Dann öffnen: http://localhost:8000/gantt-editor.html
```

## 📋 Typischer Workflow

1. **Aufgaben hinzufügen**
   - Klicken Sie auf "+ Aufgabe" oder "★ Meilenstein"
   - Füllen Sie das Formular aus (Gruppe, Name, Daten)
   - Speichern

2. **Projekt konfigurieren**
   - Gehen Sie zur Registerkarte "Konfiguration"
   - Projekttitel festlegen
   - Arbeitstage-Zählung aktivieren/deaktivieren
   - Textanzeige auf Balken konfigurieren

3. **Diagramm generieren**
   - Zurück zur Registerkarte "Aufgaben"
   - Klicken Sie auf "🎨 Diagramm generieren"
   - Das Diagramm erscheint im rechten Bereich

4. **Analyse anzeigen**
   - Wechseln Sie zur Registerkarte "Analyse"
   - Automatisch generierte Statistiken anzeigen
   - Unterbrechungen und Gruppenstatistiken prüfen

5. **Visualisierung anpassen**
   - Verwenden Sie die H/V-Zoom-Steuerungen
   - Scrollen Sie zur Navigation
   - Verwenden Sie den Zeitraumregler

6. **Speichern/Laden**
   - "💾 JSON speichern" → Konfiguration herunterladen
   - "📁 JSON laden" → Vorherige Konfiguration laden
   - "📄 Als PDF exportieren" → Diagramm als PDF speichern

## 📁 JSON-Format

Beispiel einer exportierten JSON-Datei:

```json
{
  "title": "Batteriepark Lausitz - Beispielprojekt",
  "defaultState": "BB",
  "showTextOnBars": true,
  "tasks": [
    {
      "type": "task",
      "group": "Planung",
      "name": "Standortanalyse",
      "start": "2025-11-03",
      "end": "2025-11-14",
      "duration": "10 AT",
      "tonnage": "",
      "text": "Erste Planungsphase"
    },
    {
      "type": "milestone",
      "group": "Projektstart",
      "name": "Kick-off Meeting",
      "start": "2025-11-03",
      "end": "2025-11-03",
      "duration": "",
      "tonnage": "",
      "text": ""
    }
  ]
}
```

### JSON-Felder

- **title**: Projekttitel
- **defaultState**: Bundesland-Code (momentan nur für Kompatibilität)
- **showTextOnBars**: Boolean - Text auf Balken anzeigen
- **tasks**: Array von Aufgaben/Meilensteinen
  - **type**: "task" oder "milestone"
  - **group**: Gruppenname/Phase
  - **name**: Aufgabenname
  - **start**: Startdatum (YYYY-MM-DD)
  - **end**: Enddatum (YYYY-MM-DD)
  - **duration**: Geplante Dauer (z.B. "10 AT")
  - **tonnage**: Tonnage in Tonnen (optional)
  - **text**: Text auf Balken (optional)

## 🎨 Diagramm-Steuerungen

### Zoom
- **H +/-**: Horizontale Breite erhöhen/verringern (Zeitachse)
- **V +/-**: Vertikale Höhe erhöhen/verringern (Balken)
- **⟲**: Zurücksetzen auf 100%

### Navigation
- **Horizontales Scrollen**: Navigieren bei H-Zoom > 100%
- **Vertikales Scrollen**: Mehr Aufgaben anzeigen
- **Zeitraumregler**: Zeitfenster anpassen

### Plotly-Interaktion
- **Hover**: Aufgabendetails anzeigen
- **Klick auf Legende**: Gruppen ein-/ausblenden
- **Doppelklick**: Plotly-Zoom zurücksetzen
- **Box-Auswahl**: Bereich auswählen

## 🔧 Anpassung

### Farben
Bearbeiten Sie die Funktion `generateColors()` im JavaScript:
```javascript
const colors = [
  '#3b82f6',  // Blau
  '#10b981',  // Grün
  '#f59e0b',  // Gelb
  // ... weitere hinzufügen
];
```

### Balkenhöhe
Passen Sie die Berechnung in `generateChart()` an:
```javascript
height: Math.max(500, tasks.length * 30)  // 30px pro Aufgabe
```

## ⚙️ Arbeitstage-Berechnung

Das Tool berechnet Arbeitstage wie folgt:

- **Nur Montag-Freitag** werden gezählt
- **Bundesweite deutsche Feiertage** werden ausgeschlossen:
  - Neujahr (1. Januar)
  - Karfreitag (beweglich)
  - Ostermontag (beweglich)
  - Tag der Arbeit (1. Mai)
  - Christi Himmelfahrt (beweglich)
  - Pfingstmontag (beweglich)
  - Tag der Deutschen Einheit (3. Oktober)
  - 1. Weihnachtsfeiertag (25. Dezember)
  - 2. Weihnachtsfeiertag (26. Dezember)

**Hinweis**: Bundeslandspezifische Feiertage werden momentan nicht berücksichtigt.

## 📊 Analyse-Funktionen

Die automatische Projektanalyse umfasst:

### Zeitzusammenfassung
- Reine Arbeitszeit (in Tagen und Wochen)
- Gesamte Unterbrechungszeit
- Gesamtprojektdauer

### Aufgabenübersicht
- Anzahl der Aufgaben
- Anzahl der Meilensteine
- Anzahl der Unterbrechungen

### Unterbrechungen
- Detaillierte Liste aller Lücken zwischen Aufgaben
- Dauer jeder Unterbrechung
- Aufgaben vor und nach jeder Unterbrechung

### Gruppenstatistiken
- Anzahl der Aufgaben pro Gruppe
- Arbeitszeit pro Gruppe
- Zeitspanne pro Gruppe
- Start- und Enddatum
- Auslastung (%)

## 💡 Anwendungsfälle

### ✅ Ideal für:
- Schnelle Projektplanung ohne Installationen
- Präsentationen und Demos
- Teilen mit Benutzern ohne Python
- Visuelle Projektbearbeitung
- Schnelles Prototyping
- Bauprojekte mit Tonnage-Tracking

### ⚠️ Eingeschränkt für:
- Bundeslandspezifische Feiertage
- Komplexe Ressourcenplanung
- Automatisierung mit Skripten
- Backend-Integration

## 📦 Projektdateien

```
Gantt-Diagramm-HTML/
├── gantt-editor.html          # Hauptanwendung (alles in einer Datei)
├── ejemplo-batteriepark.json  # Beispielprojekt
├── README.md                  # Diese Datei
└── LICENSE                    # Lizenz
```

## 🔮 Zukünftige Erweiterungen

Ideen zur Erweiterung des Editors:

- [ ] Bundeslandspezifische Feiertage
- [ ] Abhängigkeiten zwischen Aufgaben
- [ ] Ressourcenzuordnung
- [ ] Ressourcen-Gantt
- [ ] Verbesserte PDF-Export-Optionen
- [ ] Projektvorlagen
- [ ] Kollaborativer Modus (mit Backend)
- [ ] Kritischer Pfad-Berechnung
- [ ] Kalenderintegration

## �️ Technologie

- **HTML5** mit eingebettetem CSS und JavaScript
- **Plotly.js** für interaktive Diagramme
- **html2canvas** und **jsPDF** für PDF-Export
- Keine externen Abhängigkeiten erforderlich (CDN-Links)

## 📄 Lizenz

Siehe LICENSE-Datei im Projektverzeichnis.

## 🤝 Beitragen

Beiträge sind willkommen! Fühlen Sie sich frei, Issues zu öffnen oder Pull Requests einzureichen.

---

**Hinweis**: Dieses Tool ist für die Projektplanung mit deutschen Arbeitstagen und bundesweiten Feiertagen optimiert.
