<h1 align="center">🇩🇪 Gender Free macOS</h1>

<p align="center">
  <img src="https://user-images.githubusercontent.com/98193439/276884315-3c3efadf-b1a6-452e-b09a-eda1ff3a3eb8.png" alt="Genderfreies macOS Banner">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/macOS-Ventura%2B-blue?logo=apple" alt="macOS Ventura+">
  <img src="https://img.shields.io/badge/SIP-Filesystem%20Protections%20off-red" alt="SIP">
  <img src="https://img.shields.io/badge/Sprache-Deutsch-green" alt="Sprache">
</p>

---

> [!WARNING]
> Running this script requires that the SIP feature **“Filesystem Protections”** be disabled. Disabling this feature turns off volume signing—an important Apple security feature. Make this decision carefully and always keep a backup on hand.

## 📖 Description

Are you tired of macOS forcing gender-neutral language on you without offering an alternative? With this script, you can remove gender-neutral language from your system partition in Recovery Mode and revert to standard German.

**Prerequisite:** The SIP feature “Filesystem Protections” must be disabled.  
**Compatibility:** macOS Ventura (13.x) and later.

---

## 🚀 Schritt-für-Schritt-Anleitung

### Schritt 1 – Medium vorbereiten

Formatiere einen USB-Stick (oder nutze ein anderes Medium, z. B. das User-Verzeichnis des System Volumes) als **FAT32, exFAT, APFS oder HFS+**.

Folgende vier Dateien müssen sich immer gemeinsam in einem Ordner befinden:

```
📁 dein-medium/
├── back2normal.sh
├── suchbegriffe.txt
├── scan.sh
└── catalog.db       ← wird in Schritt 2 erzeugt
```

### Schritt 2 – Katalog erzeugen (im Live-System)

Führe **vor** dem Neustart ins Recovery `scan.sh` im laufenden System aus:

```bash
bash scan.sh
```

> Dieser Vorgang dauert einige Minuten. Die erzeugte `catalog.db` wird automatisch im selben Ordner abgelegt.

### Schritt 3 – Recovery-Modus starten

Starte deinen Mac im Recovery-Modus und öffne dort ein Terminal.

### Schritt 4 – Skript ausführen

```bash
bash /Volumes/NAME_DEINES_MEDIUMS/back2normal.sh
```

### Schritt 5 – Fertig

Sind mehrere Volumes vorhanden, wirst du gefragt, welches verwendet werden soll. Bei nur einem Volume erfolgt die Auswahl automatisch. Der Rest läuft automatisch ab – nach etwa **5–10 Minuten** ist der Prozess abgeschlossen.

---

## 🧹 Hinweis: Verbliebene Gender-Spuren entfernen

Falls Einträge wie „Benutzer:innen & Gruppen" in den Einstellungen noch sichtbar sind, hilft das kostenlose Tool **[OnyX](https://www.titanium-software.fr/en/onyx.html)**.

Nutze dort die folgende Funktion, um den **LaunchServices-Cache** neu aufzubauen:

<img width="92" height="62" alt="OnyX Funktion" src="https://github.com/user-attachments/assets/2da2bbfc-c36d-42c5-b635-6869be226c6f" />

Option:

<img width="871" height="68" alt="OnyX Option" src="https://github.com/user-attachments/assets/54f000d4-b494-48e0-aad1-dc6705c16683" />

Nach einem Neustart sind die verbliebenen Spuren verschwunden.

---

## ♻️ Wiederherstellung

Falls etwas schiefläuft, kannst du im Recovery-Modus das letzte APFS-Snapshot wiederherstellen:

```bash
bless --mount / --last-sealed-snapshot
```

---

## ⚠️ Bekannte Einschränkung

Die SIP-Funktion „Filesystem Protections" muss **dauerhaft deaktiviert** bleiben, da die Signaturen der veränderten Dateien nicht mehr mit dem Original übereinstimmen.

---

## 📝 Haftungsausschluss

> Eingriffe in das System geschehen auf **eigene Gefahr**. Es wird empfohlen, stets ein Backup parat zu haben oder das Verfahren zunächst auf einem Testsystem auszuprobieren. Es besteht **keine Haftung** für Datenverlust. Nach einem Systemupdate kann es erforderlich sein, das Skript erneut auszuführen.
