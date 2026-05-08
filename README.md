# 🗑️ Trash Lens

## Projekttitel
**Trash Lens** — Eine intelligente Bildklassifikation für Recyclable Waste

---

## 📋 Auftraggeber und Problem

Der Auftraggeber dieses Projekts ist mein Vater, der regelmässig recycelt. Dabei entstand die Idee für eine Anwendung, die beim korrekten Sortieren von Abfall helfen kann. Viele Menschen sind unsicher, wie bestimmte Materialien richtig entsorgt werden sollen, den Plastik ist nicht einfach Plastik sondern kann in weitere Kategorien unterteilt werden wie z.B. PET etc. (Einfacherhalber wurde jedoch in diesem Projekt nur eine Klasse "Plastik" aufgeführt). Falsche Mülltrennung erschwert den Recyclingprozess und führt dazu, dass recyclebare Materialien verloren gehen.

### Ziel
Eine benutzerfreundliche Web-Anwendung entwickeln, die es Nutzern ermöglicht:
- Ein Abfallbild hochzuladen ODER mit der Kamera zu fotografieren
- Das Bild automatisch in Recyclable-Kategorien zu klassifizieren
- Die Wahrscheinlichkeiten für jede Kategorie zu sehen

---

## 🎯 Kurzbeschreibung der Lösung

**Trash Lens** ist eine Progressive Web App (PWA), die auf einem trainierten Machine Learning Modell basiert. Die App:

1. **Akzeptiert zwei Input-Optionen:**
   - Datei-Upload: Benutzer wählt ein vorhandenes Bild aus
   - Kamera: Benutzer macht ein Live-Foto (mobil oder Desktop)

2. **Klassifiziert das Bild:** Ein TensorFlow.js-Modell (trainiert mit Teachable Machine) analysiert das Bild in Echtzeit im Browser

3. **Zeigt Ergebnisse:** Alle Recyclable-Kategorien mit Wahrscheinlichkeiten in % (sortiert von hoch nach niedrig)

4. **Läuft vollständig lokal:** Keine Datenübertragung an externe Server, alle Berechnungen im Browser

---

## 🌐 Öffentlicher Link zur laufenden Version

Aktuell: **Lokal gehostet** (siehe Installationsanleitung)

**Lokale URL:** `http://localhost:8000`

---

## 📖 Benutzungsanleitung

### Installation & Start

1. **Repository klonen oder Dateien herunterladen:**
   ```bash
   cd /path/to/trash-lens
   ```

2. **Lokalen Server starten:**
   ```bash
   python3 -m http.server 8000
   ```
   *(Alternativ: `python -m http.server 8000` falls Python 3 nicht funktioniert)*

3. **Im Browser öffnen:**
   ```
   http://localhost:8000
   ```

### Bedienung

1. **Wähle eine Eingabemethode:**
   - Klick **"📁 Datei hochladen"** → Wähle ein Bild von deinem Gerät
   - Oder klick **"📷 Kamera"** → Mache ein Live-Foto

2. **Warte auf die Klassifikation:**
   - Das Modell analysiert das Bild automatisch

3. **Lies die Ergebnisse:**
   - Jede Kategorie mit Wahrscheinlichkeit in %
   - Sortiert von höchster zu niedrigster Wahrscheinlichkeit

4. **Neue Klassifikation:**
   - Wechsle zwischen Upload/Kamera oder lade ein neues Bild

---

## 🤖 Beschreibung des ML-Anteils

### Modelltyp
-  Google Teachable Machine (Image Classification)
Das Projekt verwendet Machine Learning zur automatischen Klassifikation von Müllarten anhand von Bildern.

### Trainings-Daten
- **Kategorien:** Mehrere Recyclable-Materialien (Plastik, Papier, Karton, Metall, Glas und Restmüll)
- **Bilder pro Kategorie:** ~600-700 Bilder
- **Datenquellen:** Bilder aus verschiedenen Lichtsituationen und Winkeln 


### Trainings-Prozess
1. Bilder für jede Kategorie in Teachable Machine hochladen
2. Automatische Vorverarbeitung und Augmentation
3. Transfer Learning Training (ca. 5 Epochen)
4. Export als WebGL-Modell (`model.json`, `weights.bin`, `metadata.json`)

---

## 🛠️ Verwendete Tools und Libraries

| Tool/Library | Version | Zweck |
|---|---|---|
| **HTML5** | - | Struktur der Web-App |
| **CSS3** | - | Styling und Responsive Design |
| **JavaScript (ES6+)** | - | Logik und Event-Handling |
| **TensorFlow.js** | Latest | ML-Modell-Inference im Browser |
| **Teachable Machine Image Library** | Latest | Modell-Laden und Vorhersagen |
| **getUserMedia API** | Browser-Standard | Kamera-Zugriff |
| **FileReader API** | Browser-Standard | Datei-Upload-Verarbeitung |
| **Canvas API** | Browser-Standard | Bild-Verarbeitung und Foto-Capture |
| **Python** | 3.x | Lokaler HTTP-Server (Entwicklung) |

### CDN-Links
```html
<!-- TensorFlow.js -->
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>

<!-- Teachable Machine Image Library -->
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>
```

---

## 🧪 Testhinweise

### Lokale Tests
1. Starte den Server: `python3 -m http.server 8000`
2. Öffne `http://localhost:8000` im Browser
3. Teste beide Input-Methoden (Upload + Kamera)


Zum Testen können eigene Bilder von Müllobjekten verwendet werden.

Empfohlene Testbilder:
- Plastikflaschen
- Glasflaschen
- Papier
- Karton
- Metalldosen

Das Modell funktioniert am besten bei:
- guten Lichtverhältnissen
- klar sichtbaren Objekten
- neutralem bis grauen Hintergrund
- nur einem Objekt pro Bild

Zum Test:
1. Bild hochladen
2. Vorhersage des Modells anschauen
3. Überprüfen, ob die erkannte Kategorie korrekt ist

---

## ⚠️ Grenzen und bekannte Probleme

#
1. **Overfitting bei ähnlichen Klassen**
   - Verwechselt ähnliche Materialien (z.B. verwechselt braunes Papier mit Karton)
2. **Lighting-Abhängigkeit**
   - Je nach Licht verändert sich die Performance (z.B. wenn starkes Licht auf eine PET-Flasche kommt, dann wird es oft mit Glas verwechselt, wegen dem reflektierenden Effekt beider Stoffe)
3. **Hintergrund**
   - Bei farbigen Hintergründen kann die Performance ebenfalls variieren, da die Trainingsbilder lediglich graue Hintergründe hatten

---

## 📚 Quellen

### Machine Learning
- [Google Teachable Machine](https://teachablemachine.withgoogle.com/) - Modell-Training
---

## 🤖 Offenlegung: KI-Hilfsmittel

### Verwendete KI-Assistenten
- **GitHub Copilot** (Claude Haiku 4.5)

### Umfang der KI-Unterstützung
- ~70% Code wurde mit KI-Vorschlägen generiert/optimiert
- 100% des Codes wurde manuell überprüft und getestet
- KI wurde nicht für Trainings-Daten oder Modell-Architektur verwendet
- Design und Konzept sind eigenständig entwickelt, jedoch mithilfe des Agenten
---

