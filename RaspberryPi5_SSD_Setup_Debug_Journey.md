#  Raspberry Pi 5 – SSD Setup & Debugging Journey

##  Zeitleiste & Ereignisse

| Datum/Zeit       | Ereignis / Aktion                                                                 |
|------------------|------------------------------------------------------------------------------------|
| Vorbereitend     | M.2 NVMe SSD in offiziellen Raspberry Pi M.2 HAT eingebaut                         |
| Startversuch     | Raspberry Pi erkennt SSD, aber bootet nicht zuverlässig                           |
| Nächster Schritt | SD-Karte mit Raspberry Pi OS als Zwischenlösung genutzt                           |
| Installation     | Raspberry Pi OS auf SSD übertragen und gebootet über offizielle Anleitung          |
| Stabilitätscheck | Bootreihenfolge getestet: interner Port wird bevorzugt, USB-SD nicht erkannt wenn SSD steckt |
| Fazit            | Nur der integrierte M.2-Port wird stabil erkannt – USB-SD als Fallback unzuverlässig |
| Ziel             | Langfristiger Einsatz für Lernumgebung, Projekte & DevOps-Training                 |

---

##  Erkenntnisse

- **Nur der integrierte M.2-Port** wird beim Boot zuverlässig erkannt – auch wenn die SD-Karte im USB-Adapter steckt, ignoriert der Pi diese, wenn die SSD vorhanden ist.
- **Fallback mit USB-SD funktioniert nicht**, obwohl SD im USB-Port vorhanden und korrekt eingerichtet ist.
- **Bootreihenfolge hat keine Priorität**, wenn die SSD steckt – das scheint hardwarebedingt zu sein.
- Die gewählte SSD ist **SAN ZANG MASTER M.2 SSD 256GB NVMe PCIe Gen3x4 2280**. Sie wurde erkannt, hatte aber beim ersten Versuch Download-/Initialisierungsprobleme.

---

##  Nächste Schritte

- **Langzeit-Stabilität testen** (mehrfache Neustarts, Updateverhalten, Stromversorgung prüfen)
- **Heatspreader auf SSD montieren**, falls thermische Probleme auftreten
- Dokumentation zur **SSD-Kompatibilität erweitern**
- Tool-Chain für **DevOps & Lernprojekte** aufbauen:
  - Docker, Git, CI/CD, VS Code, SSH-Zugriff
  - Netzwerkzugriff absichern
  - Optional: Retropie/NAS-Projekte auf separater SD/SSD
- **Backuplösung einrichten** (z. B. mit `dd` oder `rpi-clone`)
- **TRIM-Support testen** (`fstrim -v /`), um SSD-Lebensdauer zu verlängern
- **Systemdienste automatisieren** mit Shell-Skripten (`cron`, `systemd`)

---

##  Wichtige Terminal-Kommandos

| Kommando                      | Zweck                                                               |
|------------------------------|----------------------------------------------------------------------|
| `lsblk`                      | Zeigt alle angeschlossenen Speichergeräte                           |
| `df -h`                      | Zeigt belegten Speicherplatz in verständlicher Form                 |
| `sudo raspi-config`          | Systemkonfiguration (z. B. Boot-Priorität, SSH, Sprache)             |
| `sudo apt update && upgrade` | Aktualisiert Software & System                                       |
| `cat /etc/os-release`        | Zeigt Infos zum aktuellen OS                                        |
| `sudo dd if=/dev/sda of=/dev/sdb` | Kopiert ein gesamtes Laufwerk (Backup – mit Vorsicht verwenden!) |
| `fstrim -v /`                | Manuelles Ausführen von SSD-TRIM zur Pflege der Speicherzellen      |
| `journalctl -xe`             | Zeigt Systemlogs (für Debugging hilfreich)                          |

---

##  Sichtbarkeit für Arbeitgeber?

**Ja – unter Bedingungen:**
- Der Raspberry Pi kann als **"isolierte Lernumgebung"** dokumentiert werden.
- Eignet sich als DevOps-Toolchain & Portfolio für Embedded, Netzwerk & CI/CD.
- Die **Dokumentation der Problemlösung** (Boot-Reihenfolge, Kompatibilität) zeigt **Eigeninitiative und Debugging-Fähigkeiten**.
- Wichtig: **Professioneller Ton**, keine Floskeln über „AI-Hilfe“ – sondern **konkrete Nutzung** als Unterstützung beim Troubleshooting und Lernen.

---

##  Beispielhafte Formulierung für GitHub-Projektbeschreibung

> **Ziel:** Aufbau einer isolierten Entwicklungsumgebung mit dem Raspberry Pi 5 (16 GB RAM), M.2 SSD (NVMe), und optimierter Boot-Konfiguration. Einsatz für DevOps-Training, CI/CD-Pipeline-Tests, Shell-Scripting und Netzwerkprojekte.
>
> **Lernziel:** Praktische Umsetzung und Dokumentation typischer Debugging-Prozesse bei ARM-Systemen, Bootloader-Verhalten und SSD-Kompatibilität.  
>
> **Setup-Tools:** Raspberry Pi OS (Lite), Git, Docker, VS Code (Remote SSH), Shell-Skripte zur Systemautomatisierung.

---

##  Kommentar zur AI-Nutzung

> Einige Aspekte der Dokumentation und Problemlösung wurden mithilfe von KI-gestützter Recherche verifiziert (z. B. ChatGPT).  
> Die finale Umsetzung, Tests und Debugging erfolgten jedoch vollständig selbstständig.

---

##  Fazit

Der Raspberry Pi 5 eignet sich hervorragend als **eigenständige Lern- und Entwicklungsplattform**.  
Die Entscheidung, ihn als zentrales Tool für die Umschulung und Weiterbildung einzusetzen, ist sowohl **technisch sinnvoll** als auch **strategisch gut begründet**.

---
