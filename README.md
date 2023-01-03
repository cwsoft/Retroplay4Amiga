# Pi3b-Retroplay4Amiga
Anleitung zum Erstellen einer Amiga-Retroplay Umgebung mit 2.600 Amiga Spielen für das Raspberry Pi3b. Dieses Projekt nutzt die Open-Source Software [Retropie 4.8.2](https://retropie.org.uk/download/) und [Amiberry 5.4](https://github.com/BlitterStudio/amiberry/wiki) für die Amiga-Emulation. Die Amiga Spiele entstammen dem [Retroplay's WHDLoad Archiv](https://eab.abime.net/showthread.php?t=109171) (Stand: 2023-01-03).

## Benötigte Dateien
- Raspberry Pi3B mit SD-Karte (min. 32 GB)
- [Retropie 4.8](https://retropie.org.uk/download/) für Pi 2/3 bzw. Pi 4/400
   - MD5-Pi2/3: 224e64d8820fc64046ba3850f481c87e
   - MD5-Pi4/400: b5daa6e7660a99c246966f3f09b4014b
- Amiga Emulator [Amiberry](https://github.com/BlitterStudio/amiberry/wiki)
- Legale Amiga Kickstart Roms z.B. [AmigaForever Plus](https://www.amigaforever.com/plus/)
- Amiga Spieldateien (z.B. ADF, LHA) z.B. [WHDownload](https://www.whdownload.com/)

## A: Retropie auf SD-Karte installieren (PC)
1. Retropie-Image für Pi-Modell herunterladen und Checksumme prüfen
   `certutil -hashfile <imgage.gz> MD5`
2. Retropie-Image (.gz) auf SD-Karte schreiben (z.B. [RPi Imager](https://www.raspberrypi.com/software/) oder [balenaEtcher](https://www.balena.io/etcher/))
3. Optional: `wifikeyfile.txt` in SD-Boot-Partition (/boot) erstellen
   ```
   ssid="xy" -> xy:=WLAN-Netzwerk
   psk="xy" -> xy:=WLAN-Passwort
   ```

## B: Retropie Grundeinstellungen (Pi)
1. SD-Karte in Pi einstecken, USB-Controller anschließen und booten
2. Tastatur-Bedienung für Emulation-Station (nachfolgend ES) einrichten
   - Eine beliebige Taste auf der angeschlossenen Tastatur länger drücken
   - D-Pad: Cursor-Tasten (hoch/runter/links/rechts)
   - Start: S, Select: M
   - Button A / EAST: Eingabetaste (Enter)
   - Button B / SOUTH: Escape (Esc)
   - Button X: X (ES: Random)
   - Button Y: Y (ES: Favorites)
   - alle Tasten bis auf vorletzte überspringen (beliebige Taste z.B. Leertaste länger drücken)
   - Hotkey: H (letzte Taste)
   - mit Enter (OK) abschliessen
3. Controller-Bedienung für ES einrichten (z.B. "The C64 Joystick", bzw. "CompetionPro")
   - S drücken -> Configure Input wählen
   - Beliebige Taste eines Controllers länger drücken
   - D-Pad: Joystick hoch/runter, links/rechts
   - Start: kleiner Dreieck-Knopf links, Select: kleiner Dreieck-Knopf rechts
   - Button A / EAST: Feuertaste links
   - Button B / SOUTH: Feuertaste rechts
   - alle anderen Tasten überspringen (belegte Taste z.B. Feuertaste links länger drücken)
   - mit Leertaste (OK) abschliessen
4. Schritt 3 für weitere Controller wiederholen
5. Zur RetroPie Configuration wechseln (Esc, Enter) -> RASPI-CONFIG aufrufen (Pfeiltasten + Enter)
   - [5] Localisation Einstellungen ändern:
     - L1: Locale -> de_DE.UTF-8 als Standard
     - L2: Timezone auf Europe/Berlin ändern
     - L3: Keyboard (Generic 105-key -> Other -> German -> German, Standartwerte akzeptieren)
     - L4: WLAN Country (DE Germany)
   - RASPI-CONFIG beenden (Finish) -> neu starten
6. Zur RetroPie Configuration wechseln (Enter) -> WIFI aufrufen (Pfeiltaste + Enter)
   - [3] Import WiFi credentials from /boot/wifikeyfile.txt (vgl. Schritt A.4),
     ODER [1] Connect to WiFi Network (SSID und Passphrase eingeben)
   - Internetverbindung prüfen (IP Adresse und ESSID wird angezeigt)
   - WIFI-SETUP verlassen (Exit)

## C: Amiberry installieren (Pi)
1. RETROPIE SETUP (Pfeiltasten + Enter)
2. OPTIONAL: [U] Update Packages (ca. 15-20 Minuten) 
3. [S] Update Retropie-Setup Script (4.8.2 oder höher)
4. [P] Manage packages eingeben
   - [opt] Manage optional packages
   - [4] amiberry -> install from pre-compiled binary (aktuell v5.4)
5. Retropie neu starten (Back, Back, Back, Perform reboot)
6. Amiga auswählen (es sollte ein Eintrag mit "+START AMIBERRY") vorhanden sein
7. Mit Esc ins Hauptmenü wechseln

Hinweis: Amiberry kann auch von "Source" kompiliert werden. Hierzu mit Nano in `/home/pi/RetroPie-Setup/scriptmodules/emulators/amiberry.sh` die Version anpassen. Eintrag `rp_module_repo=` suchen und gewünschte Version eintragen wie `rp_module_repo="git https://github.com/BlitterStudio/amiberry v5.x|master"`.

## D: Amiga ROMs und Spiele kopieren (PC)
Die notwendigen Amiga Kickstart ROMs können legal z.B. von Cloanto [AmigaForever Plus](https://www.amigaforever.com/plus/) erworben werden. Das Plus-Paket enthält alle gängigen Kickstart ROMs für die Amiga Modelle A500-A4000 und einige Spiele im ADF format. Viele alte Spiele finden sich als vorinstallierte LHA-Dateien (WHDLoad) heute im Internet z.B. [WHDownload](https://www.whdownload.com/).

1. Auf Windows PC Explorer öffnen (WIN+E)
2. Mit Retropie verbinden (\\retropie in Explorer-Adressleiste)
3. Folgende Kickstart Roms (z.B. Amiga Forever) nach bios\amiga kopieren:
   - amiga-os-310-a1200.rom (Voraussetzung für WHDLoad)
   - amiga-os-130.rom (A500 Spiele)
   - amiga-os-205-a600.rom (Kompatibilität)
   - rom.key (ältere AF-Versionen)
   - Optional: amiga-os-310-a600.rom, amiga-os-310-a4000.rom
4. Spiele (.adf, .lha) nach roms\amiga kopieren (empfohlen: .lha, WHDLoad)
5. ES neu starten (Taste S -> Quit -> Restart ES)

## E: Amiberry Anpassungen
1. ES -> Amiga -> +Start Amiberry klicken
2. Tab Paths wechseln: Rescan Paths, Update WHDLoad XML -> Update Controller DB klicken -> Quit
3. Zur Console wechseln (Taste S -> Quit -> Quit ES -> Yes)
4. Amiberry Git Repo klonen und AmiQuit kopieren (fehlt in Retropie Amiberry bis v5.4)
   ```
   cd ~
   git clone https://github.com/BlitterStudio/amiberry
   cp ~/amiberry/whdboot/AmiQuit /opt/retropie/emulators/amiberry/whdboot
   
   OPTIONAL (z.B. Amiberry selbst kompilieren):
   cd amiberry
   make clean
   make -j2 PLATFORM=rpi3
   ```
5. Amiberry config anpassen:
   ```
   nano /opt/retropie/emulators/amiberry/conf/amiberry.conf
   default_quit_key=F11
   default_horizontal_centering=yes
   default_vertical_centering=yes
   default_auto_crop=no
   default_whd_quit_on_exit=yes
   ```
6. ES neu starten (Console: exit + Enter -> Amiga)
   
## F: Controller Feuerknopf-Zuordnung anpassen
Ein Zwei-Spieler-Spiel starten und prüfen ob Feuerknöpfe links/rechts getauscht werden müssen, falls ja ...
1. Zur Console wechseln (Taste S -> Quit -> Exit ES)
2. `jstest /dev/input/js0` (Joystick Port 0)
   Linken/rechten Feuerknopf drücken und Button-Nummern notieren (z.B. links: btn->0, rechts: btn->1)
3. `jstest /dev/input/js1` (Joystick Port 1)
   Linken/rechten Feuerknopf drücken und Button-Nummern notieren (z.B. links: btn->3, rechts: btn->0
3. `cd /opt/retropie/configs/all/retroarch-joypads`
4. nano " THE C64*.cfg" (Joystick Port 0)
   input_b_btn = "1"  --> input_b_btn = "0"
   input_a_btn = "0"  --> input_a_btn = "1"
   STRG+X -> J -> Enter -> Speichern
5. nano "SPEEDLINK COMPETION*.cfg" (Joystick Port 1)
   input_b_btn = "0"  --> input_b_btn = "3"
   input_a_btn = "3"  --> input_a_btn = "0"
   STRG+X -> J -> Enter -> Speichern
   
Beim nächsten ES-Start sind in WHDLoad/ADF Spielen die Feuertasten vertauscht.
   
## G: Amiga Feeling Tweaks
1. Start-Menü beim Spielstart deaktivieren
   - Retropie Setup -> [C] Configuration / tools -> [225] runcommand
     [1] Launch menu (disable)
     [2] Launch menu art (disable)
     [4] Launch image delay (3s)
     Copy launching.png|jpg file to each configs/emulator to show launch image instead
2. Splashscreen beim Hochfahren anzeigen
   - Copy splashscreen image or video to /splashscreens Samba folder
   - Retropie Config -> Splash Screens -> [1] Choose splashscreens -> [2] Own/Extra splashscreens -> Select file
3. Spiel-Infos und Vorschaubilder erstellen
   - ES -> S -> Scrapper -> Scrape Now
   Hinweis: WHDLoad Spiele werden oft nicht korrekt erkannt. Input -> Enter -> alles bis auf Spielname löschen.
   Optional: skyscraper installieren und von der Kommandozeile einlesen.
4. Raspberry Pi Rainbow screen deaktivieren
   ```
   sudo nano /boot/config.txt
   [all]
   disable_splash=1
   ```
5. Raspberry Pi Konsolenausgaben unterdrücken, blinkenden Cursor deaktivieren
   ```
   sudo nano /boot/cmdline.txt
   vt.global_cursor_default=0 quiet (Zeilenende hinzufügen)
   ```

## H: Retroplay WHDLoad Game Pack
WHDLoad sollte mit vorinstallierten [LHA-Spielen](https://www.whdownload.com/) funktionieren. 
 - https://whdload.de/ (Infos zu Trainern, eigene lha-Dateien erstellen, enthält keine Spieldateien!!)
 - https://www.whdownload.com/ (vorinstallierte LHA-Spiele)
 - https://www.planetemu.net/roms/commodore-amiga-games-adf (ADF Spiele)
 - https://www.lemonamiga.com/games/votes_list.php (Übersicht der 100 beliebtesten Amiga-Spiele nach Genre)

Wer nicht gerne selbst LHA-Dateien herunterlädt, kann auf fertige Packete (z.B. Retroplay) zurückgreifen. Das Retroplay WHDLoad Game Archiv enthält etwa 4.739 Amiga Spiele (Stand 2023-01-03). Wie das relativ komfortabel geht, wird nachfolgend beschrieben.

1. PC: WHDLoad Game Pack vom TurranFtp Server herunterladen
   - [EAB-Infos TurranFTP Server](https://eab.abime.net/showthread.php?t=61028)
   - [EAB-Infos: WHDLoad Tool](https://eab.abime.net/showthread.php?t=109171) (Sort A-Z, PAL, Englisch)

2. PC: Alle WHDLoad Ordner (0,A-Z) nach `\\retropie\roms\amiga` kopieren

3. PI: Skyscraper installieren
   - [Retropie Skyscraper Installation](https://retropie.org.uk/docs/Scraper/#lars-muldjords-skyscraper)
   - [Skyscraper Infos](https://github.com/muldjord/skyscraper/blob/master/docs/CLIHELP.md)
   
4. PI: Skysraper Konfigurieren und Spieldaten scrapen
   - ES beenden, zu Konsole wechseln
   - `sudo ~/Retropie-Setup/retropie_setup.sh`
   - [C] Configuration / tools -> skyscraper
   - [3] Cache Options and commands -> Enable Cache screenshots/covers and scrap only missing
   - [2] Gather source: Open Retro / The Games DB / Screenscraper (findet 2427/2460 Spielen)
   - [1] Gather resources (dauert je nach Spielen mehrere Stunden)
   - [4] Generate game list(s)
   
### Troubleshoting Amiga-Spiele-Namen
Ggf. werden die Amiga-Spiele-Namen nur als gekürzter Dateiname angezeigt. Dann kann folgendes Abhilfe schaffen.

1. Skyscraper Konfigurationsdatei ändern
In der Datei `~/.skyscraper/config.ini` folgende Werte im Abschnitt [main] ändern:
brackets="false"
forceFilename="false"

2. Skyscraper Prioritätenliste ändern
In der Datei `~/.skyscraper/cache/amiga/priorities.xml` die Reihenfolge der Scraper für "title" wie folgt ändern:
`Screenscraper, thegamesdb, openretro, esgamelist, arcadedb, mobygames, import`

3. Game list generation options ändern (Skyscraper Menü)
Im Skyscraper Menü (siehe vorheriger Punkt 4) folgende Optionen ändern:
[5] Generate options 
    - [1] ROM Names (Source name)
	- [2] Remove bracket info (Enabled)
	- [3] Use ROM folders for game list & media (Disabled)
	
Danach die ES Game Liste neu erstellen lassen [4] Generate game list(s), nun sollten Spielnamen vernünftig formatiert sein.