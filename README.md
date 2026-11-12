# BC Unified QoL Patch

An unofficial fan patch for **Star Trek: Bridge Commander** (2002). One patched `stbc.exe` fixes and modernises the game, and a graphics layer comes with it. No game or mod script is replaced: the changes run in memory, from the exe and a few new script files. It works on the stock 1.1 game (CD, no-CD or GOG exe), with or without the 4 GB patch, and with mods that keep the stock scripts in place.

This started as years of slow solo work on a game I love. Over the last few weeks, working with Claude and Codex on the game's own exe, it has moved faster than ever, and there's a lot more on the way.

## Download

Get the latest version from **[Releases](../../releases/latest)**. Each release has the patch zip and its What's New.

This repo holds releases only. It contains no game files, so you need your own copy of Bridge Commander.

## Highlights

- **Two torpedo systems.** Ships that carry two kinds of torpedo can now fire them separately. A second torpedo panel shows each system's tubes and reloads, and the X key fires the second system. It works in single player, co-op and multiplayer.
- **Multithreading.** The game now uses spare CPU cores for two heavy jobs: sorting which ships are near each other, and working out hull damage from hits. Big battles no longer freeze for seconds at a time. In our 81-ship test, the worst freeze dropped from 6 seconds to 0.04 seconds.
- **Preload Extended.** Big effect and ship textures go to the graphics card during the loading screen, so the first explosion or weapon hit no longer stutters.
- **Co-op (beta).** Play together on one mission. The crew joins the lobby and picks their seats before the host engages. You see each other's targets, and the crew seat gets the bridge view.
- **New LCARS screens.** Configure, Quick Battle with a 3D ship preview, New Game, Load Game, Multiplayer, the quit dialog, a loading screen with a progress bar, and Startup and Shutdown Sequences.
- **Modern graphics.** SGSSAA anti-aliasing, bloom, HDR, per-pixel lighting, ship shadows, colour grading, modern ship highlights on the GPU, and more. Every effect has its own switch.
- **Texture compression.** Textures load from compressed DDS, so they use far less video memory (5.5 GB down to 3.4 GB in our tests).
- **Performance Overlay.** FPS, frame times, every CPU core, the GPU, and the game's memory and address space.

## Everything the patch does

### Display and video
- Widescreen resolutions up to 3840x2160 in the game's own list (only sizes your display reports).
- The HUD, LCARS panels, fonts and weapon markers fit your screen at any resolution, including after a change in game.
- Widescreen field of view (Hor+). 4:3 looks exactly as before.
- Borderless windowed mode, with big resolutions no longer greyed out.
- A VSync option, fullscreen and windowed.
- A 24-bit depth buffer, so far less flicker where surfaces meet.
- Menu videos fall back to the largest one that fits, and the Bink video DLL is made crash-safe in memory.
- The 1080 intro, logo, credits and end-game movies play cleanly in fullscreen.
- Skip Intro Video option.
- Faster windowed mode and loading screens: the picture stays on the graphics card.
- Smooth motion even after the PC has been on for days (no UptimeFaker needed).

### Controls
- The mouse moves 1:1, with no camera over-rotation and no lost slow movements.
- Bridge head-look follows the mouse 1:1 (stock was about 7x too fast).
- The mouse wheel scrolls menu lists everywhere.
- Separate mouse speed and field of view for Tactical and the Bridge, applied at once.
- Bridge camera shake jolts away from the side that was hit, then settles. A switch and a strength slider control it.

### Gameplay
- Two torpedo systems (see Highlights).
- Phaser beams scroll at the speed the ship's hardpoint sets, and tractor beams use the hardpoint's own colours and texture.
- Torpedo spreads home in sooner (0.5 s instead of 2 s, adjustable).
- Weapon hits always light the hull, even on big ships like the Borg cube.
- AI speed-up: AI ships with torpedo evasion off skip the unused torpedo watcher.
- Bridge crew keep their seats after a quit and reload, on every bridge.
- Weapon fire is no longer dropped in multiplayer.

### Performance
- Multithreading (see Highlights). It picks 0, 1 or 2 helpers for your CPU.
- Preload Extended (see Highlights).
- Big battles stay faster for longer: explosions and hit effects reuse their old slots instead of piling up. Late in a long fight that is about 5% more FPS on average, and more near the end.
- Texture compression, with the DDS files made by the exe on first launch.
- Textures leave the graphics card when you leave a mission.
- A memory helper: a 64-bit helper program that the game can move big data to when its 4 GB space gets tight. Its settings are in Configure.

### Graphics
- SGSSAA anti-aliasing.
- Effects, each with its own switch: Glow Bloom, HDR Scene (FP16), Glow Shimmer Fix, Per-Pixel Lighting, Deband, Rim Light, Ship Shadows, Colour Grade, Planet Glow and Heat Ripple.
- Modern ship highlights, worked out on the GPU (about 7.5% faster).
- DXVK (Vulkan) set up automatically when your PC supports it.

### Sound
- High Quality sound: 64 voices, all Full HRTF, at 44.1 kHz.

### LCARS screens
- A new LCARS Configure, with sliders, profiles, a Mod Menus page and live previews from the in-battle Esc menu.
- LCARS main menu top bar, New Game, Load Game, Multiplayer (with an in-game Esc page) and the quit dialog.
- A new LCARS Quick Battle that reads your install's own ships and regions (no Foundation needed), with a 3D ship preview.
- Faster, sharper LCARS menus: they react at once, and nothing from the stock menus shows or reacts behind them.
- Startup Sequence: an LCARS "incoming transmission" opening around the 1080 movie.
- Shutdown Sequence: the screen powers down piece by piece when you quit.
- A loading screen with a progress bar that learns how long each load takes. You can use your own picture.
- Orion compatibility: the Orion Theme Selector, mutators and Wave Defense show up when Orion Delta RC4.1 is installed.

### Co-op (beta)
- A co-op lobby: the crew joins and picks seats, then the host engages.
- Shared targeting, the bridge view for crew, and join and leave lines in chat.
- Co-op Skirmish, plus Waves as a test mode.

### Stability, safety and logs
- Crash guards for known stock crashes (freed objects, failed allocations, Python None, a 16 MB main thread stack), plus fixes for crashes on quit, on changing Sound Quality and on skipping the intro.
- A crash when you went Configure > resolution > Multiplayer is fixed.
- No crash after the intro on mods like KM.
- The patcher finds other graphics wrappers (dgVoodoo, ReShade) and Windows compatibility mode, which crash the game, and offers to move them aside. Undo puts them back.
- One log switch, a log per channel, a crash log with details, and the logs of your last 5 runs kept.
- An optional 4 GB (Large Address Aware) flag.
- Undo puts everything back.

## What's to come

- **Download ships in game.** Browse and install ships from inside Bridge Commander.
- **A new hull damage system.** Hull damage drawn with real depth on the ships. The masking is ready.
- **New suns.** Stars that look and behave like stars, including novas.
- **PlanetFX.** New planets, already used in our cutscenes, coming to the game.
- **Planet landings.** Early work started. They'll use texture streaming (below), so they can be done the modern way rather than in an older style.
- **Volumetric effects.** Explosions, shockwaves, fires and warp with real depth. This one is next. It was close to finished and should have been in this release, but lost backups and a bug set it back.
- **Texture streaming.** Big textures loaded as they're needed, so heavy mods and HD packs fit.
- **Network code upgrades.** Easier hosting with automatic port opening, and steadier online play. Already started.
- **Co-op campaign.** The story missions played together.
- **Bridge co-op for roleplay groups.** Each player takes a station on the same ship (Helm, Tactical, Science, Engineering) and the captain gives the orders.
- **Mission scripter.** Place ships, set objectives, and write the hails and story beats for your own crew.
- **More screen setups.** A station console on a second monitor, the view across several monitors, or a tablet as a station panel.
- **VR.** The captain's chair, on the bridge.
- **The LCARS app.** One app to install, update and manage the patch and its add-ons.
- And a lot more.

## Install

1. Unzip the patch. The easiest place is inside the game folder, next to `stbc.exe`. If it can't find `stbc.exe`, it asks you to pick it.
2. Windows 10/11: run `PATCH.bat`. It uses the PowerShell built into Windows, so there's nothing else to install. If Windows blocks it, right-click the zip, choose Properties, tick Unblock, then unzip.
3. Linux (Steam/Proton, Lutris, Wine): run `./patch.sh`.
4. To remove it, run `UNDO.bat` (Linux: `./patch.sh undo`).

The README inside the zip has the full details, every off switch, and what has been tested.

## Problems

Run `COLLECT-LOGS.bat` (Linux: `./patch.sh logs`) and send the zip it makes.
