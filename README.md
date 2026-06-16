# 7Loader

7Loader ist ein Windows-Desktop-Launcher für **7 Days to Die**. Die Anwendung startet das Spiel, verwaltet Spielprofile, synchronisiert profilbezogene Spielstände und Welten, installiert Mods aus `7daystodiemods.com` und speichert Server für den direkten Beitritt.

Das Projekt ist eine WPF-Anwendung auf Basis von `.NET 10` mit dem Assembly-Namen `7Loader` und dem Root-Namespace `SevenLoader`.

## Hauptfunktionen

- **Spielstart**: Startet 7 Days to Die aus dem konfigurierten Installationsordner. Je nach Profil wird Anti-Cheat bevorzugt über `start_protected_game.exe` bzw. `7DaysToDie_EAC.exe` oder ohne Anti-Cheat über `7DaysToDie.exe` gestartet.
- **Startoptionen**: Unterstützt globale Parameter wie News-Screen überspringen, Intro überspringen, randloses Fenster, Quick Continue, Spielsprache, XInput deaktivieren, native Eingabe deaktivieren, GameSense deaktivieren und eigene Startargumente.
- **Profile**: Erlaubt mehrere Spielprofile mit eigenem Namen, Icon, Anti-Cheat-Einstellung und Mod-Zuweisungen.
- **Profil-Spielstände**: Synchronisiert pro Profil die Ordner `Saves`, `GeneratedWorlds` und `SavesLocal` aus `%APPDATA%\7DaysToDie`. Vorhandene Live-Daten werden vor dem Start gesichert und nach dem Spielende wiederhergestellt.
- **Mod-Verwaltung**: Lädt Mod-Daten von `https://7daystodiemods.com/discover`, zeigt Details, Kategorien, Versionen, Bilder, Dateigrößen und Update-Hinweise an.
- **Mod-Downloads**: Lädt Mod-Archive mit Fortschrittsanzeige herunter, speichert lokale Manifeste und legt optionale Offline-Bilder ab.
- **Mod-Installation**: Entpackt aktuell `.zip`-Archive, sucht installierbare Ordner mit `ModInfo.xml` und kopiert die dem aktiven Profil zugewiesenen Mods vor dem Spielstart in den `Mods`-Ordner des Spiels.
- **Server**: Speichert Servername, Adresse, Port, optionales Passwort und Favoritenstatus. Der Beitritt erfolgt über eine `steam://connect/...`-URI.
- **Darstellung und Sprache**: Bietet ein dunkles und helles Theme sowie deutsche und englische Ressourcen.
- **Startfenster**: Zeigt beim Programmstart ein eigenes Ladefenster mit Fortschritt und Statusmeldungen.

## Datenablage

7Loader speichert seine eigenen Daten unter:

```text
%APPDATA%\7Loader
```

Wichtige Unterordner und Dateien:

- `settings.json`: Einstellungen, Profile, Server, Sprache, Theme und Startoptionen.
- `Mods\`: Heruntergeladene und installierte Mods inklusive `mod.json`-Manifesten.
- `Cache\`: Mod-Katalog, Suchparameter, Mod-Details und Übersetzungs-Cache.
- `Profiles\`: Profilbezogene Spielstände und Welten.
- `Backups\`: Sicherungen vorhandener Live-Spielstände.
- `Runtime\active-session.json`: Laufende oder wiederherzustellende Spielsitzung.

Beim Start kann ein vorhandener alter Datenordner `%APPDATA%\7DtD Launcher` automatisch nach `%APPDATA%\7Loader` migriert werden, sofern noch kein neuer 7Loader-Ordner existiert.

## Externe Dienste

Die Anwendung nutzt Netzwerkzugriff für:

- `https://7daystodiemods.com`: Mod-Katalog, Mod-Detailseiten und Downloads.
- `https://api.7daystodiemods.com`: API-basierte Download-Auflösung, wenn die Webseite entsprechende Daten bereitstellt.
- `https://api.mymemory.translated.net`: Optionale Übersetzung von Mod-Beschreibungen.

Kataloge, Detailtexte und Übersetzungen werden lokal gecacht, damit bereits geladene Informationen wiederverwendet werden können.

## Voraussetzungen

- Windows
- .NET SDK 10.0 oder neuer mit Windows-Desktop-Unterstützung
- Eine lokale Installation von 7 Days to Die
- Netzwerkzugriff, wenn Mod-Katalog, Downloads oder Übersetzungen genutzt werden sollen

## Laufzeitverhalten

Beim Start lädt 7Loader Einstellungen, Theme, Sprache, Profile, Server, Mod-Cache und vorhandene installierte Mods. Falls kein Spielpfad gespeichert ist, versucht die Anwendung, typische Steam-Installationspfade und Steam-Bibliotheken zu durchsuchen. Ein gültiger Spielordner muss eine passende 7-Days-to-Die-Startdatei enthalten.

Beim Spielstart bereitet 7Loader zuerst die Profil-Spielstände vor, kopiert die dem Profil zugewiesenen Mods in den Spielordner und startet danach das Spiel oder den Serverbeitritt. Nach dem Beenden des Spiels speichert 7Loader die geänderten Profil-Daten zurück, räumt den Live-Datenordner auf und stellt vorher vorhandene Originaldaten wieder her.

## Hinweise

- Mod-Archive müssen aktuell als `.zip` vorliegen. Andere Archivformate werden abgelehnt.
- Installierbare Mods werden über `ModInfo.xml` erkannt.
- Der Launcher ersetzt den `Mods`-Ordner im Spielordner staging-basiert, damit nur die Mods des aktiven Profils aktiv sind.
- Die Anwendung speichert Änderungen an Einstellungen, Profilen und Servern unmittelbar.
- Es sind keine separaten Testprojekte im Repository vorhanden.
