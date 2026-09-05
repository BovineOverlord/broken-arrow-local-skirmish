# Broken Arrow — Local Skirmish

A [MelonLoader](https://github.com/LavaGang/MelonLoader) mod that turns Broken Arrow's **Skirmish** button
into a real, **fully-local battle against the AI** — with a proper setup panel for map, deck, difficulty
and the map's own game options. No online lobby, no anti-cheat, no network required.

> **Single-player / offline only.** This is for offline modded play (EasyAntiCheat off). It does **not**
> enable online multiplayer with a modded client. It's a fan-made mod, not affiliated with or endorsed by
> the developers or publisher of Broken Arrow.

---

## Install (the easy way)

1. Click the green **Code ▸ Download ZIP** button above and unzip it anywhere.
2. Double-click **`install.bat`**.

The installer finds your Broken Arrow install, **downloads and installs MelonLoader v0.7.3 for you** if it
isn't already there, copies the mod into `Mods\`, and adds a **"Broken Arrow (Modded)"** desktop shortcut.

Launch the game with that desktop shortcut (not the Steam Play button — that runs EasyAntiCheat, which
blocks mods), then click **Skirmish**.

> The first modded launch is slower because MelonLoader generates the game's code assemblies once. A black
> MelonLoader console window opening alongside the game is normal.

## How to use

1. Launch modded (the "Broken Arrow (Modded)" shortcut).
2. In the main menu, click **Skirmish**. Instead of the dead online lobby, a **Local AI Skirmish** setup
   panel opens.
3. Choose your **map**, **deck**, **difficulty**, and any map-specific options (income, time limit,
   day/night, map size, …), then **Start Battle**.

You spawn in with your deck against the scenario's AI opponents (and any AI allies it defines). Everything
runs on your machine.

## What it actually does (and why)

Clicking Skirmish normally calls the online lobby backend, which fails offline (HTTP 400 with anti-cheat
off). The built-in `*_Skirmish` maps also ship with **empty slots** — the online lobby is what fills in
nations, decks and AI/human assignments — so launching one offline loads terrain but spawns nothing.

Instead, the mod uses the **36+ pre-configured offline-vs-AI scenarios** the game already ships
(`ScenarioType.MultiplayerPVE` battles and singleplayer missions), whose slots already have a human slot
plus AI bots with decks and nations baked in. It intercepts the lobby call and launches the chosen scenario
locally through the game's own scene-transition path — exactly how the game's own local scenario launcher
works. Real multiplayer (Rating / Custom) is left completely untouched.

## Limits

- **Offline only** — it does not create real online lobbies with a modded client.
- It uses the game's PvE scenarios, not the original empty `*_Skirmish` maps (those can't be configured for
  a local match without rebuilding the whole online lobby).
- Difficulty and the map's public options are honoured; your first valid deck for the map is preselected and
  you can change it in the panel.

## Uninstall

Delete `Mods\BALocalSkirmish.dll`. To remove the loader entirely, delete `version.dll` and the
`MelonLoader\` folder from the game directory.

## Build it yourself / extend it

See **[docs/MODDING.md](docs/MODDING.md)** for how the mod works, the game hooks it uses, and how to compile
from source.

## License

[MIT](LICENSE) © 2026 BovineOverlord. Provided as-is, with no warranty. Use at your own risk; you are
responsible for complying with the game's own terms of service.
