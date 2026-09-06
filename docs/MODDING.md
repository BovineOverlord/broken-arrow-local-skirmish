# Modding guide: BA Local Skirmish

How the mod works and how to build/extend it.

## How it works

The mod is a single MelonLoader `MelonMod` that Harmony-patches one method:

- **`NetworkLobbyService.CreateLobby`**, when the lobby type is `Skirmish`, the prefix cancels the original
  (which would try to reach the online backend) and instead opens an in-game setup panel built with Unity UI.
  Rating/Custom lobby types fall through untouched.

When you press **Start Battle**, the mod:

1. lists the game's offline scenarios via `ScenariosService`, `ScenarioType.MultiplayerPVE` and
   `Singleplayer`, which already have a human slot plus AI bots with decks and nations,
2. places your chosen deck into `PreloadSharedPlayerDeck` (`ScenarioStartDeck` / `Alpha` / `Bravo`), exactly
   like the game's own local launcher,
3. sets difficulty on `CampaignService.Difficulty`,
4. pushes the map's public-option choices into `SceneLoadManager.ScenarioPublicOptions`,
5. calls `ISceneTransition.ChangeScene(scenario)` to start the battle locally.

Key game types (all under `Il2CppBrokenArrow.*`, browsable in the generated
`MelonLoader\Il2CppAssemblies\Il2CppBrokenArrow.dll`):

- `Client.Ecs.GNetwork.Services.Lobby.NetworkLobbyService`, the patched entry point.
- `MissionEditor.MissionResolver.ScenariosService` / `ScenarioSource` / `ScenarioType`, the scenario list.
- `Client.Ecs.UI.ISceneTransition`, `Client.Ecs.Utils.SceneLoadManager`, launching the scene.
- `Client.Ecs.Decks.DeckService`, `Client.Ecs.Decks_v2.PreloadSharedPlayerDeck`, deck selection/preload.
- `Client.Ecs.Campaign.CampaignService`, `Shared.Ecs.Enums.DifficultyLevel`, difficulty.

## Extending it

The whole UI and launch flow is in `src/LocalSkirmish.cs`:

- **Change what the Skirmish button does**, `CreateLobbyPatch.Prefix` and `Core.OpenSetup`.
- **Setup panel controls**, `BuildUI` / `Row(...)`; map/deck/difficulty/option cycling is in
  `CycleMap`, `CycleDeck`, `CycleDiff`, `CycleOpt`.
- **Which scenarios are offered**, `BuildMapList` (currently PvE + singleplayer). Filter or reorder there.
- **How a battle is launched**, `StartBattle`.

## Building from source

**Prerequisites**

- Windows, with the game installed.
- [.NET SDK 6.0 or newer](https://dotnet.microsoft.com/download).
- MelonLoader installed and the game launched **once** modded, so `MelonLoader\Il2CppAssemblies\` exists
  (running `install.bat` from the repo root installs MelonLoader for you).

**Build**

```powershell
dotnet build -c Release src\BALocalSkirmish.csproj -p:GameDir="D:\Games\Broken Arrow"
```

Point `-p:GameDir` at your own install (or edit the default `<GameDir>` line in `src\BALocalSkirmish.csproj`).
The output `BALocalSkirmish.dll` lands in `src\bin\Release\`. Copy it into the game's `Mods\` folder, or
overwrite `dist\BALocalSkirmish.dll` and re-run `install.bat`.

## Verifying at runtime

`MelonLoader\Latest.log` shows, on launch:

```
Patched CreateLobbyPatch
```

and when you click Skirmish / start a battle:

```
[LocalSkirmish] Skirmish clicked -> opening setup panel.
[LocalSkirmish] Setup opened (N maps).
[LocalSkirmish] Launching '<scenario>' deck '<deck>' with M option(s).
```
