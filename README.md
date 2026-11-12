# BC Unified QoL Patch

[![Windows: supported](https://img.shields.io/badge/Windows-supported-2ea44f?logo=windows&logoColor=white)](#install)
[![Linux: supported](https://img.shields.io/badge/Linux%20(Proton%2FWine)-supported-2ea44f?logo=linux&logoColor=white)](#install)
[![macOS: coming soon](https://img.shields.io/badge/macOS-coming%20soon-lightgrey?logo=apple&logoColor=white)](#whats-to-come)
[![Latest release](https://img.shields.io/github/v/release/acidtwin/STBC-Remastered-Patch?include_prereleases&label=latest%20release)](../../releases/latest)
[![Game: Star Trek Bridge Commander](https://img.shields.io/badge/game-Star%20Trek%3A%20Bridge%20Commander%20(2002)-blue)](#)
[![Works on stock 1.1, GOG, Remastered 2.0, Orion Delta, Legacy 1.0, Kobayashi Maru and more](https://img.shields.io/badge/works%20on-stock%201.1%20%7C%20GOG%20%7C%20Remastered%202.0%20%7C%20Orion%20Delta%20%7C%20Legacy%201.0%20%7C%20Kobayashi%20Maru%20%7C%20and%20more-blue)](#)

An unofficial fan patch for **Star Trek: Bridge Commander** (2002). One patched `stbc.exe` fixes and modernises the game, and a graphics layer comes with it. No game or mod script is replaced: the changes run in memory, from the exe and a few new script files. It works on the stock 1.1 game (CD, no-CD or GOG exe), with or without the 4 GB patch, and with mods that keep the stock scripts in place: Remastered 2.0, Remastered Orion (Orion Delta), Legacy 1.0, Kobayashi Maru and many more.

I've been tinkering with this game since not long after it came out in 2002. It started with hacking `Effects.py`, and my first camera work lived in there too, long before it had a name. For most of those years it was all just for me. I mostly lurked, apart from now and then trying to push my Effects file on people. Discord got me properly involved, and the serious work began in 2023 with my first video, with Claude and Codex helping along the way. This is the first time I've really shared any of it. Recently, a much deeper understanding of the game's own exe has sped it up more than ever, and there's a lot more on the way.

## Download

Get the latest version from **[Releases](../../releases/latest)**. Each release has the patch zip and its What's New.

This repo holds releases only. It contains no game files, so you need your own copy of Bridge Commander.

## Highlights

- **Widescreen done right, inside the exe.** Real widescreen resolutions, Hor+ field of view, and a HUD and fonts sized for your screen, all built into `stbc.exe`. No extra plugin needed. 4:3 looks exactly as before.
- **Two torpedo systems.** Ships that carry two kinds of torpedo can now fire them separately. A second torpedo panel shows each system's tubes and reloads, and the X key fires the second system. It works in single player, co-op and multiplayer.
- **64-bit Memory Helper.** Bridge Commander is a 32-bit game, so everything it loads has to fit in 4 GB of address space, and big mods and HD textures run out of room. The patch adds a separate 64-bit helper program, `bchost.exe`, that holds big data outside the game's 4 GB and hands it back when the game needs it. By default it holds up to 2 GB of your PC's RAM, and on real Windows it has held 3.27 GB in testing. It's a normal visible file next to the game, nothing hidden or packed. If it's missing or stops, the game carries on without it. You can turn it on or off in Configure, and the Performance Overlay shows how much it holds.
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
- Widescreen field of view (Hor+), built into the exe from AlphaYellow's FOV fix. 4:3 looks exactly as before.
- Your real graphics card name is shown, and the z-buffer is on for every card.
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
- Big-battle CPU fixes in the exe: sparse scene lists, scene-bound scanning and proximity pair removal. Around 30% less main-thread work in big battles, before the helper threads even start.
- Preload Extended (see Highlights).
- Big battles stay faster for longer: explosions and hit effects reuse their old slots instead of piling up. Late in a long fight that is about 5% more FPS on average, and more near the end.
- Texture compression, with the DDS files made by the exe on first launch. An LCARS progress window shows while they convert.
- Effect textures stay loaded between missions, so nothing rebuilds mid-battle.
- Textures leave the graphics card when you leave a mission.
- 64-bit Memory Helper (see Highlights).

### Graphics
- SGSSAA anti-aliasing.
- Effects, each with its own switch: Glow Bloom, HDR Scene (FP16), Glow Shimmer Fix, Per-Pixel Lighting, Deband, Rim Light, Ship Shadows, Colour Grade, Planet Glow and Heat Ripple.
- Modern ship highlights, worked out on the GPU (about 7.5% faster).
- DXVK (Vulkan) set up automatically when your PC supports it.
- Effects never draw over the menus or the HUD.
- The Performance Overlay comes in four sizes, with rows for the Memory Helper.

### Sound
- High Quality sound: 64 voices, all Full HRTF, at 44.1 kHz.

### LCARS screens
- A new LCARS Configure, with sliders, profiles, a Mod Menus page and live previews from the in-battle Esc menu.
- LCARS main menu top bar, New Game, Load Game, Multiplayer (with an in-game Esc page) and the quit dialog.
- A new LCARS Quick Battle that reads your install's own ships and regions (no Foundation needed), with a 3D ship preview.
- Spectate mode in Quick Battle, with its own camera, so you can sit back and watch the fight.
- Early cinematic cameras, optional: F7 Duel Cam and F8 War Correspondent. More to come.
- Glass LCARS: backlit "light box" panels with a sheen, sharp fonts in every LCARS menu, and a calmer backdrop when you open Configure in battle.
- Faster, sharper LCARS menus: they react at once, and nothing from the stock menus shows or reacts behind them.
- Startup Sequence: an LCARS "incoming transmission" opening around the 1080 movie.
- Shutdown Sequence: the screen powers down piece by piece when you quit.
- A loading screen with a progress bar that learns how long each load takes. You can use your own picture.
- Orion compatibility: the Orion Theme Selector, mutators and Wave Defense show up when Orion Delta RC4.1 is installed.

### Co-op (beta)
- Host and join from our own LCARS screen instead of the stock multiplayer screens.
- A co-op lobby: the crew joins and picks seats, then the host engages. Each seat can be crew, AI or closed.
- Join a game already in progress, with a file check so everyone runs the same thing.
- Shared targeting, the bridge view for crew, and join and leave lines in chat.
- Co-op Skirmish, plus Waves as a test mode.

### Stability, safety and logs
- Crash guards for known stock crashes (freed objects, failed allocations, Python None, a 16 MB main thread stack), plus fixes for crashes on quit, on changing Sound Quality and on skipping the intro.
- Save games fixed: saving had quietly broken in the stock game. It works again, and saves from before the patch still load.
- The game's own crash writer no longer crashes itself, so you get a proper crash report.
- A crash when you went Configure > resolution > Multiplayer is fixed.
- No crash after the intro on mods like KM.
- The patcher finds other graphics wrappers (dgVoodoo, ReShade) and Windows compatibility mode, which crash the game, and offers to move them aside. Undo puts them back.
- One log switch, a log per channel, a crash log with details, and the logs of your last 5 runs kept.
- An optional 4 GB (Large Address Aware) flag.
- Undo puts everything back.

### The patcher
- One patcher for Windows and Linux, with DXVK on or off.
- It backs up what it changes, and Undo restores only its own backups.
- It writes a receipt of the version it installed.
- Every exe change is checked against the stock bytes first. Nothing is applied blind.

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
- **CameraNX.** Cinematic cameras that frame the battle like a space shot from the show.
- **VR.** The captain's chair, on the bridge.
- **The LCARS app.** One app to install, update and manage the patch and its add-ons.
- **An optional mod pack.** Extras that sit outside the core patch, such as sound upgrades, for players who want them.
- And a lot more.

## Thanks

**Code this patch is built on**
- **AlphaYellow**: the widescreen FOV fix (MIT), now built into the exe.
- **elishacloud**: dxwrapper (zlib), which the graphics chain runs on.
- **DXVK** by Philip Rebohle and contributors (zlib), for Vulkan.

**The Bridge Commander community**
- **VonFrank**, for Bridge Commander: Remastered.
- **Denacity**, for Bedrock.
- **Orion**, for Orion Delta.
- **Michael Wiley**, for the Dauntless and his ships.
- **Whiskers**, for testing on Windows and in co-op.
- **Cuddly**, for the 64-voice sound tip.
- **Nocturnal** and **Tethys**.
- Everyone who tested, sent logs and put up with broken builds.

**The Morrowind modding community**
- MGE XE, Greatness7's 64-bit helper work and OpenMW showed what an old engine can be pushed to do. Our Memory Helper follows the same idea, and their open work helped this project a lot.

## Install

1. Unzip the patch. The easiest place is inside the game folder, next to `stbc.exe`. If it can't find `stbc.exe`, it asks you to pick it.
2. Windows 10/11: run `PATCH.bat`. It uses the PowerShell built into Windows, so there's nothing else to install. If Windows blocks it, right-click the zip, choose Properties, tick Unblock, then unzip.
3. Linux (Steam/Proton, Lutris, Wine): run `./patch.sh`.
4. To remove it, run `UNDO.bat` (Linux: `./patch.sh undo`).

The README inside the zip has the full details, every off switch, and what has been tested.

## Problems

Run `COLLECT-LOGS.bat` (Linux: `./patch.sh logs`) and send the zip it makes.
