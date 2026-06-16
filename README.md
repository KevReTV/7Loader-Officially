# 7Loader

7Loader is a Windows desktop launcher for **7 Days to Die**. It helps you start the game, keep separate play profiles, switch profile-specific saves and worlds, install mods, and store servers for quick joining.

German version: [README.de.md](README.de.md)

## Requirements

- Windows 10 or newer
- A local installation of **7 Days to Die**
- **.NET SDK 10.0 for Windows** is required and is not included in this publish package. Download it from the official Microsoft .NET page: [Download .NET 10.0](https://dotnet.microsoft.com/en-us/download/dotnet/10.0)
- Internet access is required for the mod catalog, mod downloads, and optional translation features.

## Included Files

This publish folder contains the runnable 7Loader application.

- `7Loader.exe`: starts the launcher
- `README.md`: English user guide
- `README.de.md`: German user guide

Depending on the build, debug files such as `7Loader.pdb` may also be present. They are not required for normal use.

## First Start

1. Install the required .NET SDK 10.0 if it is not already installed.
2. Start `7Loader.exe`.
3. Select your **7 Days to Die** installation folder if 7Loader does not find it automatically.
4. Create or select a profile.
5. Configure launch options, mods, and servers as needed.

7Loader looks for common Steam installation paths and Steam library folders. A valid game folder must contain the normal 7 Days to Die launch files.

## Main Features

- **Game launch**: Starts 7 Days to Die from the configured installation folder.
- **Anti-Cheat control**: Uses the protected game launcher when Anti-Cheat is enabled for the active profile, or starts the normal game executable when Anti-Cheat is disabled.
- **Launch options**: Supports options such as skipping the news screen, skipping the intro, borderless window mode, quick continue, game language, disabled XInput, disabled native input, disabled GameSense, and custom launch arguments.
- **Profiles**: Stores multiple game profiles with their own name, icon, Anti-Cheat setting, assigned mods, and profile data.
- **Profile saves and worlds**: Keeps profile-specific copies of `Saves`, `GeneratedWorlds`, and `SavesLocal` from `%APPDATA%\7DaysToDie`.
- **Mod catalog**: Loads mod information from `7daystodiemods.com`, including details, categories, versions, images, file sizes, and update notes.
- **Mod downloads**: Downloads mod archives with progress display and stores local manifests for installed mods.
- **Mod installation**: Extracts `.zip` archives, detects installable mods through `ModInfo.xml`, and copies the mods assigned to the active profile into the game's `Mods` folder before launch.
- **Servers**: Stores server name, address, port, optional password, and favorite status. Servers are joined through a `steam://connect/...` link.
- **Appearance and language**: Provides dark and light themes as well as English and German application text.

## Data Location

7Loader stores its own data here:

```text
%APPDATA%\7Loader
```

Important files and folders:

- `settings.json`: settings, profiles, servers, language, theme, and launch options
- `Mods\`: downloaded and installed mods, including local `mod.json` manifests
- `Cache\`: mod catalog cache, search data, mod details, and translation cache
- `Profiles\`: profile-specific saves and worlds
- `Backups\`: backups of existing live save data
- `Runtime\active-session.json`: information about a running or recoverable game session

If an older `%APPDATA%\7DtD Launcher` folder exists and `%APPDATA%\7Loader` does not yet exist, 7Loader can migrate the old data folder automatically.

## How Profile Data Works

Before starting the game, 7Loader prepares the active profile:

1. Existing live game data is backed up.
2. The active profile's saves and worlds are placed into the normal 7 Days to Die data folder.
3. The active profile's selected mods are copied into the game's `Mods` folder.
4. The game is started.

After the game closes, 7Loader stores changed saves and worlds back into the active profile, cleans up the live data folder, and restores any original live data that existed before launch.

## External Services

7Loader uses network access for these services:

- `https://7daystodiemods.com`: mod catalog, mod pages, and downloads
- `https://api.7daystodiemods.com`: API-based download resolution when available
- `https://api.mymemory.translated.net`: optional translation of mod descriptions

Catalog entries, details, and translations are cached locally where possible.

## Notes

- Mod archives must currently be `.zip` files.
- Installable mods are detected through `ModInfo.xml`.
- The launcher prepares the game's `Mods` folder for the active profile before starting the game.
- Settings, profiles, and servers are saved immediately when changed.
