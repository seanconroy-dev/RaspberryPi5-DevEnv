# Raspberry Pi 5 – SSD Setup & Debugging Journey

## Was & Warum?

**Ziel:** Aufbau eines stabilen Raspberry-Pi-5-Systems mit SSD als primärem Speichermedium, um ein isoliertes, zuverlässiges und portables Lernsystem zu schaffen.  
Dieses Setup begleitet mich beim beruflichen Umstieg in die Softwareentwicklung & DevOps – mit Fokus auf Java, TypeScript, Markdown, Shell, GitHub-Dokumentation und systemnahem Arbeiten.  
Das System soll Entwicklungsumgebungen, Tools und Projekte lokal bereitstellen, unabhängig von Cloud oder Work-PCs.

---

## Zeitleiste & Ereignisse

| Datum/Zeit       | Ereignis / Aktion                                                                 |
|------------------|------------------------------------------------------------------------------------|
| Vorbereitend     | M.2 NVMe SSD in offiziellen Raspberry Pi M.2 HAT eingebaut                         |
| Start            | SSD wurde erkannt, aber initialer Boot instabil                                   |
| Boot-Versuche    | Erst über SD-Karte gebootet, dann Versuch OS auf SSD zu schreiben                  |
| Fehler           | SSD-Boot friert ein, keine Reaktion auf Tastatur/Maus nach Desktop-Start           |
| Hotplug-Versuch  | SSD im laufenden Betrieb eingesteckt – funktioniert unzuverlässig                  |
| Wiederaufbau     | SD-Karte neu geflasht mit 64-bit OS Full (~3 GB) über Raspberry Pi Imager          |
| Analysephase     | Frühere Images (~1.1 GB) evtl. zu minimal – Wechsel auf vollständige Version       |
| Erfolg           | SSD korrekt beschrieben, reibungsloser Boot & stabile Performance                  |

---

## Realisierte Erkenntnisse

- **Nur SD-Karten im integrierten Leser** werden als „boot-priorisiert“ erkannt.  
- **SD-Karte via USB** wird nur erkannt, wenn **kein anderes Medium (SSD)** vorhanden ist.  
- Wenn sowohl SSD als auch SD (USB) eingesteckt sind, **überschreibt SSD die Bootpriorität**, selbst wenn SD in `raspi-config` bevorzugt ist.
- Der Imager erkennt SSDs nicht im Live-Betrieb, wenn davon gebootet wurde.
- Minimale OS-Versionen (z. B. 1.1 GB) enthalten wichtige Tools und Dienste nicht.
- Der interne SD-Port ist für Bootreihenfolge zwingend – USB-SD ist nicht gleichwertig.

---

## Reflexionen

- Ursprüngliche Probleme waren schwer einzugrenzen – Kombination aus Hardware-Prioritäten, Imagequalität und Toolset.
- Die Wahl des „empfohlenen“ Images war trügerisch – nicht voll ausgestattet.
- SSD ließ sich nur stabil betreiben, wenn korrekt geflasht, formatiert und mit vollem OS beschrieben.
- Die Hardware-Priorisierung des Bootloaders ist nicht flexibel dokumentiert – erfordert Erfahrung oder gezielte Recherche.
- Diese Erfahrung spiegelt reale DevOps-Herausforderungen wider: Diagnose, Wiederherstellung, Automatisierung und zuverlässige Systeme.

---

## AI-Unterstützung

Die gesamte technische Reise wurde durchgängig mit ChatGPT begleitet – in Echtzeit, strukturiert und problemorientiert.  
Ich nutzte KI aktiv für:

- Bootanalyse und Prioritätslogik  
- Recherche zu OS-Größen und Tool-Verfügbarkeit  
- Terminal-Kommandos zur Diagnose und Bestätigung  
- Reflektierende Dokumentation und Wissensaufarbeitung  

Ich setze KI gezielt ein, um technische Zusammenhänge schneller zu durchdringen, Lösungen eigenständig zu erarbeiten und Arbeitsprozesse effizient zu dokumentieren – ein praxisnaher Ansatz, der mir hilft, komplexe Aufgaben im DevOps-Umfeld schrittweise souverän zu meistern.

---

## Wichtige Terminal-Kommandos

| Kommando                      | Zweck                                                                 |
|------------------------------|----------------------------------------------------------------------|
| `lsblk`                      | Listet alle erkannten Laufwerke auf                                  |
| `cat /etc/os-release`        | Zeigt Infos über das aktuelle Betriebssystem                         |
| `sudo raspi-config`          | Konfiguration von Boot, Sprache, SSH usw.                            |
| `sudo apt update && upgrade` | Aktualisiert Paketliste und installierte Software                    |
| `sudo apt install <paket>`   | Installiert Programme (z. B. `git`, `code`, `openjdk-17-jdk`)        |
| `df -h`                      | Zeigt belegten Speicherplatz in lesbarer Form                        |
| `mount` / `umount`           | Laufwerke manuell ein-/aushängen                                     |
| `journalctl -xe`             | Zeigt Systemfehler und Logs (fortgeschrittene Diagnose)              |

---

## Genutzte Tools & Pakete

- VSCodium / VS Code
- OpenJDK 17
- Git
- Curl
- apt-basiertes Paketmanagement

---

## Erkenntnisse

- "Recommended OS" ≠ vollständiges OS – für Entwicklung Full-Image (3 GB) verwenden.
- SSD muss korrekt geflasht und formatiert werden.
- Pi Imager erkennt SSD nicht im laufenden Betrieb, wenn davon gebootet wurde.
- Pi Apps / Shop verschwand bei Lite- oder Minimalversionen.
- Debian 64-bit unterscheidet sich im vorinstallierten Toolset.
- Nur **integrierter SD-Port** ist für konsistente Boot-Priorisierung zuverlässig.

---

## Noch offen

- SSD auf TRIM-Funktion prüfen
- Backuplösung einrichten (z. B. via `dd` oder `rpi-clone`)
- Bootloader-Tiefe besser verstehen
- SSD-Kompatibilität langfristig testen

---

*Letzte Aktualisierung: 15.07.2025*

