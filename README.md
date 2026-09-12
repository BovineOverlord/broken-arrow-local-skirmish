# Broken Arrow: Local Skirmish

A MelonLoader mod that turns Broken Arrow's **Skirmish** button into a real, **fully-local battle against
the AI**, with a proper setup panel for map, deck, difficulty and the map's own game options. No online
lobby, no anti-cheat, no network required.

> **Single-player / offline only.** This is for offline modded play (EasyAntiCheat off). It does not enable
> online multiplayer with a modded client. It's a fan-made mod, not affiliated with or endorsed by the
> developers or publisher of Broken Arrow.

---

## Install (the easy way)

1. Click the green **Code** button above and choose **Download ZIP**, then unzip it anywhere.
2. Double-click **`install.bat`**.

The installer finds your Broken Arrow install, **downloads and installs MelonLoader v0.7.3 for you** if it
isn't already there, copies the mod into `Mods\`, writes `steam_appid.txt` + a Steam-aware launcher, and adds
a **"Broken Arrow (Modded)"** desktop shortcut.

**Make sure Steam is running and signed in**, then launch the game with that desktop shortcut (not the Steam
Play button, which runs EasyAntiCheat and blocks mods), then click **Skirmish**.

> **Steam must be running.** The shortcut starts the game with anti-cheat off but still with a Steam context.
> Without it (e.g. Steam closed, or launching the raw exe on a fresh install) the game hangs at the
> "Loading Hangar" screen. The launcher makes sure Steam is up first.
>
> The first modded launch is slower because MelonLoader sets itself up once. A black MelonLoader console
> window opening alongside the game is normal.

## How to use

1. Launch modded (the "Broken Arrow (Modded)" shortcut).
2. In the main menu, click **Skirmish**. A **Local AI Skirmish** setup panel opens.
3. Choose your **map**, **deck**, **difficulty**, and any map-specific options (income, time limit,
   day/night, map size), then **Start Battle**.

You spawn in with your deck against the AI opponents (and any AI allies the scenario defines). Everything
runs on your machine.

## Pairs with the Balance Mod

If you also install the [Balance Mod](https://github.com/BovineOverlord/broken-arrow-balance-mod), your
rebalanced stats apply in these local battles. (The Balance Mod needs Local Skirmish to give it an offline
battle to play in, so if you want custom stats, install both.)

## Limits

- **Offline only.** It does not create real online lobbies with a modded client.
- **Which maps.** The panel lists the maps that can be played vs AI offline: the built-in **PvE / co-op**
  scenarios and **campaign** missions (plus any Workshop co-op scenarios you've installed). Plain multiplayer
  / `*_Skirmish` maps are **not** listed — they ship with empty player slots that only the online lobby fills,
  so they can't be populated with an army + AI offline. Many MP terrains do have a PvE version that *is* listed
  (Kaliningrad, Narva, Daugavpils, Ignalina, Coal Mountain, River, Ruda, Klaipeda, Parnu, Baltiysk, Refinery).
  To play a specific MP terrain vs AI, make a PvE scenario on it in the in-game mission editor and it'll appear.
- Difficulty and the map's options are honoured. Your first valid deck for the map is preselected, and you
  can change it in the panel.

## Uninstall

Delete `Mods\BALocalSkirmish.dll`. To remove the loader entirely, delete `version.dll` and the
`MelonLoader\` folder from the game directory.

## Build it yourself / extend it

See **[docs/MODDING.md](docs/MODDING.md)** for how to compile from source.

## License

[MIT](LICENSE), 2026 BovineOverlord. Provided as-is, with no warranty. Use at your own risk; you are
responsible for complying with the game's own terms of service.
