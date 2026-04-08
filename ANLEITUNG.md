# Transkription App — Bauanleitung für Maestras

Deine eigene Transkriptions-App: Audio & Video zu Text, kostenlos, in Sekunden.

---

## Was du brauchst

1. **Groq API-Key** (kostenlos) → [console.groq.com](https://console.groq.com)
2. **GitHub Account** (kostenlos) → [github.com](https://github.com)
3. **Netlify Account** (kostenlos) → [netlify.com](https://app.netlify.com)

Zeitaufwand: 5–10 Minuten (Weg A) oder ca. 60 Minuten (Weg B)

---

## Weg A: Fork & Deploy (schnell, 5 Minuten)

Du kopierst die fertige App und veröffentlichst sie unter deiner eigenen URL.

### Schritt 1: Groq API-Key holen

1. Gehe auf [console.groq.com](https://console.groq.com)
2. Registriere dich (kostenlos, keine Kreditkarte nötig)
3. Klicke links auf **API Keys** → **Create API Key**
4. Kopiere den Key (fängt mit `gsk_` an) — den brauchst du später in der App

### Schritt 2: Repository forken

1. Gehe auf [github.com/CryptoManuela/transkription-app](https://github.com/CryptoManuela/transkription-app)
2. Klicke oben rechts auf **Fork**
3. Klicke **Create fork**
4. Du hast jetzt eine eigene Kopie des Codes auf deinem GitHub

### Schritt 3: Auf Netlify veröffentlichen

1. Gehe auf [app.netlify.com](https://app.netlify.com)
2. Logge dich ein (oder registriere dich kostenlos)
3. Klicke **Add new project** → **Import an existing project**
4. Wähle **GitHub** und autorisiere den Zugriff
5. Wähle dein Repository **transkription-app**
6. Alles auf Standard lassen → **Deploy**
7. Nach ca. 30 Sekunden bekommst du deine URL (z.B. `dein-name-transkription.netlify.app`)

### Schritt 4: App nutzen

1. Öffne deine neue URL
2. Gib deinen Groq API-Key ein → Speichern
3. Ziehe eine Audio- oder Videodatei rein
4. Klicke **Transkription starten**
5. Fertig — dein Transkript erscheint und kann als .txt heruntergeladen werden

### Optional: URL anpassen

In Netlify unter **Site configuration** → **Change site name** kannst du die URL ändern, z.B. `mein-name-transkription.netlify.app`.

---

## Weg B: Selbst bauen mit Claude Code (Lernprojekt, ~60 Min)

Du baust die App Schritt für Schritt mit Claude Code. Maximaler Lerneffekt!

### Vorbereitung

1. **Groq API-Key** holen (siehe Weg A, Schritt 1)
2. **GitHub Account** anlegen und in Claude Code einloggen:
   ```
   ! gh auth login -p https -w
   ```
3. **Netlify Account** anlegen und in Claude Code einloggen:
   ```
   ! npm install -g netlify-cli
   ! netlify login
   ```

### Prompt 1: Projekt erstellen

Kopiere diesen Prompt in Claude Code:

> Erstelle einen neuen Ordner `transkription-app` mit einem Git-Repo. Erstelle darin folgende Dateien:
>
> 1. `index.html` — Eine schöne, moderne Single-Page-App mit:
>    - Eingabefeld für einen Groq API-Key (wird in localStorage gespeichert)
>    - Drag & Drop Upload für Audio/Video-Dateien (MP3, MP4, M4A, WAV)
>    - Sprachauswahl (Deutsch, Englisch, etc.)
>    - Modellauswahl (Whisper Large v3 und Whisper Large v3 Turbo)
>    - Checkbox für optionale Timestamps
>    - Fortschrittsbalken
>    - Ergebnis-Textarea mit Kopieren- und Download-Button
>    - DSGVO-Hinweis dass Audio an Groq (USA) gesendet wird
>
> 2. `css/style.css` — Modernes, elegantes Design
>
> 3. `js/app.js` — Die komplette Logik:
>    - API-Key in localStorage speichern und laden
>    - Datei-Upload per Drag & Drop und Klick
>    - Große Dateien (>24MB) in Chunks aufteilen
>    - Direkte Fetch-Calls an die Groq Whisper API (https://api.groq.com/openai/v1/audio/transcriptions)
>    - Ergebnis anzeigen, kopieren und als .txt downloaden
>    - Bei aktivierten Timestamps: Zeitstempel vor jedem Segment anzeigen
>
> 4. `netlify.toml` — Minimale Netlify-Konfiguration (publish = ".")
>
> 5. `.gitignore` — node_modules, .env, .netlify
>
> Halte den Code einfach und gut kommentiert.

### Prompt 2: Testen

> Starte einen lokalen Server damit ich die App im Browser testen kann.

Claude Code wird vermutlich `npx serve .` oder `python -m http.server` vorschlagen. Öffne die angezeigte URL im Browser und teste mit einer kurzen Audiodatei.

### Prompt 3: Auf GitHub & Netlify veröffentlichen

> Erstelle ein GitHub-Repo namens "transkription-app" und pushe den Code. Deploye die App dann auf Netlify.

### Prompt 4: Anpassen (optional)

Jetzt kannst du die App nach deinen Wünschen anpassen:

> Ändere die Farben zu [deine Farben]. Ändere den Titel zu [dein Titel]. Füge mein Logo ein.

Oder:

> Füge eine Option hinzu, die das Transkript als Zusammenfassung formatiert.

Jede Änderung deployst du mit:

> Pushe die Änderungen auf GitHub und deploye auf Netlify.

---

## Tipps & Tricks

### Groq Rate Limits (kostenloser Free Tier)
- **2 Stunden Audio pro Stunde** — reicht für einen 90-Minuten-Call
- Limit wird stündlich zurückgesetzt
- Tipp: **Zero Data Retention** in den [Groq-Einstellungen](https://console.groq.com/settings/data) aktivieren (Datenschutz!)

### Dateigröße
- Groq akzeptiert max. **25 MB** pro Datei (Free Tier)
- Die App teilt größere Dateien automatisch auf
- Tipp: Audio-Dateien (MP3, M4A) sind viel kleiner als Video (MP4)

### Unterstützte Formate
MP3, MP4, M4A, WAV, OGG, WEBM

### Funktioniert auf jedem Gerät
- Mac, Windows, Linux — egal
- Sogar auf dem Handy (Datei über "Auswählen" statt Drag & Drop)
- Kein Install nötig, läuft komplett im Browser

---

## Häufige Fragen

**Ist das wirklich kostenlos?**
Ja. Groq Free Tier, GitHub Free, Netlify Free — alles kostenlos.

**Sieht jemand meinen API-Key?**
Nein. Der Key ist nur in deinem eigenen Browser gespeichert. Wenn jemand anders deine App-URL öffnet, muss die Person ihren eigenen Key eingeben.

**Was passiert mit meinen Audio-Dateien?**
Die Datei wird zur Transkription an Groq-Server in den USA gesendet. Mit aktiviertem Zero Data Retention werden keine Daten bei Groq gespeichert.

**Wie gut ist die Transkription?**
Whisper Large v3 ist eines der besten Transkriptionsmodelle weltweit — besonders gut für Deutsch. Nicht perfekt bei starkem Dialekt oder schlechter Audioqualität, aber für Meetings und Gespräche ausgezeichnet.

---

*Gebaut mit Whisper (OpenAI) via Groq API · © 2026 Manuela Ruppert · KI Maestra*
*Co-Created with Claude Code by Anthropic*
