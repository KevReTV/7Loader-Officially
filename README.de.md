# 7Loader

7Loader ist ein Windows-Desktop-Launcher fuer **7 Days to Die**. Das Programm hilft dir dabei, das Spiel zu starten, getrennte Spielprofile zu nutzen, profilbezogene Spielstaende und Welten umzuschalten, Mods zu installieren und Server fuer den schnellen Beitritt zu speichern.

English version: [README.md](README.md)

## Voraussetzungen

- Windows 10 oder neuer
- Eine lokale Installation von **7 Days to Die**
- **.NET SDK 10.0 fuer Windows** wird benoetigt und ist in diesem Publish-Paket nicht enthalten. Lade es ueber die offizielle Microsoft-.NET-Seite herunter: [Download .NET 10.0](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
- Internetzugriff wird fuer den Mod-Katalog, Mod-Downloads und optionale Uebersetzungen benoetigt.

## Enthaltene Dateien

Dieser Publish-Ordner enthaelt die ausfuehrbare 7Loader-Anwendung.

- `7Loader.exe`: startet den Launcher
- `README.md`: englische Anleitung
- `README.de.md`: deutsche Anleitung

Je nach Build koennen auch Debug-Dateien wie `7Loader.pdb` enthalten sein. Fuer die normale Nutzung werden sie nicht benoetigt.

## Erster Start

1. Installiere das benoetigte .NET SDK 10.0, falls es noch nicht installiert ist.
2. Starte `7Loader.exe`.
3. Waehle deinen **7 Days to Die**-Installationsordner aus, falls 7Loader ihn nicht automatisch findet.
4. Erstelle oder waehle ein Profil.
5. Richte Startoptionen, Mods und Server nach Bedarf ein.

7Loader sucht nach typischen Steam-Installationspfaden und Steam-Bibliotheksordnern. Ein gueltiger Spielordner muss die normalen Startdateien von 7 Days to Die enthalten.

## Hauptfunktionen

- **Spielstart**: Startet 7 Days to Die aus dem konfigurierten Installationsordner.
- **Anti-Cheat-Steuerung**: Nutzt den geschuetzten Spielstarter, wenn Anti-Cheat im aktiven Profil eingeschaltet ist, oder startet die normale Spiel-EXE, wenn Anti-Cheat ausgeschaltet ist.
- **Startoptionen**: Unterstuetzt Optionen wie News-Screen ueberspringen, Intro ueberspringen, randloses Fenster, Quick Continue, Spielsprache, deaktiviertes XInput, deaktivierte native Eingabe, deaktiviertes GameSense und eigene Startargumente.
- **Profile**: Speichert mehrere Spielprofile mit eigenem Namen, Icon, Anti-Cheat-Einstellung, zugewiesenen Mods und Profildaten.
- **Profil-Spielstaende und Welten**: Verwaltet profilbezogene Kopien von `Saves`, `GeneratedWorlds` und `SavesLocal` aus `%APPDATA%\7DaysToDie`.
- **Mod-Katalog**: Laedt Mod-Informationen von `7daystodiemods.com`, inklusive Details, Kategorien, Versionen, Bildern, Dateigroessen und Update-Hinweisen.
- **Mod-Downloads**: Laedt Mod-Archive mit Fortschrittsanzeige herunter und speichert lokale Manifeste fuer installierte Mods.
- **Mod-Installation**: Entpackt `.zip`-Archive, erkennt installierbare Mods ueber `ModInfo.xml` und kopiert die dem aktiven Profil zugewiesenen Mods vor dem Spielstart in den `Mods`-Ordner des Spiels.
- **Server**: Speichert Servername, Adresse, Port, optionales Passwort und Favoritenstatus. Der Beitritt erfolgt ueber einen `steam://connect/...`-Link.
- **Darstellung und Sprache**: Bietet dunkles und helles Theme sowie englische und deutsche Programmtexte.

## Datenablage

7Loader speichert seine eigenen Daten hier:

```text
%APPDATA%\7Loader
```

Wichtige Dateien und Ordner:

- `settings.json`: Einstellungen, Profile, Server, Sprache, Theme und Startoptionen
- `Mods\`: heruntergeladene und installierte Mods inklusive lokaler `mod.json`-Manifeste
- `Cache\`: Mod-Katalog-Cache, Suchdaten, Mod-Details und Uebersetzungs-Cache
- `Profiles\`: profilbezogene Spielstaende und Welten
- `Backups\`: Sicherungen vorhandener Live-Spielstaende
- `Runtime\active-session.json`: Informationen zu einer laufenden oder wiederherstellbaren Spielsitzung

Wenn ein alter Ordner `%APPDATA%\7DtD Launcher` existiert und `%APPDATA%\7Loader` noch nicht vorhanden ist, kann 7Loader den alten Datenordner automatisch migrieren.

## So funktionieren Profildaten

Vor dem Spielstart bereitet 7Loader das aktive Profil vor:

1. Vorhandene Live-Spieldaten werden gesichert.
2. Die Spielstaende und Welten des aktiven Profils werden in den normalen 7-Days-to-Die-Datenordner gelegt.
3. Die ausgewaehlten Mods des aktiven Profils werden in den `Mods`-Ordner des Spiels kopiert.
4. Das Spiel wird gestartet.

Nachdem das Spiel geschlossen wurde, speichert 7Loader geaenderte Spielstaende und Welten zurueck in das aktive Profil, raeumt den Live-Datenordner auf und stellt zuvor vorhandene Originaldaten wieder her.

## Externe Dienste

7Loader nutzt Netzwerkzugriff fuer diese Dienste:

- `https://7daystodiemods.com`: Mod-Katalog, Mod-Seiten und Downloads
- `https://api.7daystodiemods.com`: API-basierte Download-Aufloesung, wenn verfuegbar
- `https://api.mymemory.translated.net`: optionale Uebersetzung von Mod-Beschreibungen

Katalogeintraege, Details und Uebersetzungen werden nach Moeglichkeit lokal gecacht.

## Hinweise

- Mod-Archive muessen aktuell `.zip`-Dateien sein.
- Installierbare Mods werden ueber `ModInfo.xml` erkannt.
- Der Launcher bereitet den `Mods`-Ordner des Spiels vor jedem Start fuer das aktive Profil vor.
- Einstellungen, Profile und Server werden direkt gespeichert, sobald sie geaendert werden.
