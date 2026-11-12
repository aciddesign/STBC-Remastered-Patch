# BC Unified QoL Patch

[![Windows: supported](https://img.shields.io/badge/Windows-supported-2ea44f?logo=windows&logoColor=white)](#install)
[![Linux: supported](https://img.shields.io/badge/Linux%20(Proton%2FWine)-supported-2ea44f?logo=linux&logoColor=white)](#install)
[![Steam Deck: coming soon](https://img.shields.io/badge/Steam%20Deck-coming%20soon-lightgrey?logo=steamdeck&logoColor=white)](#whats-to-come)
[![macOS: coming soon](https://img.shields.io/badge/macOS-coming%20soon-lightgrey?logo=apple&logoColor=white)](#whats-to-come)
[![Latest release](https://img.shields.io/github/v/release/acidtwin/STBC-Remastered-Patch?include_prereleases&label=latest%20release)](../../releases/latest)
[![Game: Star Trek Bridge Commander](https://img.shields.io/badge/game-Star%20Trek%3A%20Bridge%20Commander%20(2002)-blue)](#)
[![Works on stock 1.1, GOG, Remastered, Orion Delta, Legacy 1.0, Kobayashi Maru and more](https://img.shields.io/badge/works%20on-stock%201.1%20%7C%20GOG%20%7C%20Remastered%20%7C%20Orion%20Delta%20%7C%20Legacy%201.0%20%7C%20Kobayashi%20Maru%20%7C%20and%20more-blue)](#)

An unofficial fan patch for **Star Trek: Bridge Commander**. One patched `stbc.exe` plus a graphics layer. No game or mod script is replaced, everything runs in memory. Works on stock 1.1 (CD, no-CD, GOG), with or without the 4 GB patch, and on mods that keep the stock scripts: Remastered, Remastered Orion (Orion Delta), Legacy 1.0, Kobayashi Maru and many more.

**Best experience: VonFrank's Bridge Commander: Remastered.** It's the recommended base and the one I build on, out of respect for what VonFrank has done for the community.

I've tinkered with BC since not long after it came out, mostly just for myself, hacking `Effects.py` and lurking. Discord got me involved, the serious work started in 2023, and Claude and Codex have helped along the way. This is the first time I've really shared any of it.

## Download

Grab the latest from **[Releases](../../releases/latest)** (patch zip + What's New). No game files here, you need your own copy.

## Install

1. Unzip the patch, easiest inside the game folder next to `stbc.exe` (it asks if it can't find it).
2. Windows 10/11: run `PATCH.bat`. Nothing else to install. If Windows blocks it: right-click the zip, Properties, tick Unblock, unzip again.
3. Linux (Steam/Proton, Lutris, Wine): run `./patch.sh`.
   Tested on, and works best with, **Proton-CachyOS** (SLR build `proton-cachyos-slr-20261005`).
4. Remove: `UNDO.bat` (Linux: `./patch.sh undo`).

Full details, every off switch and what's been tested are in the README inside the zip.

## Highlights

- **Widescreen done right, in the exe.** Real widescreen resolutions, Hor+ FOV, HUD and fonts sized to your screen. No plugin needed. 4:3 unchanged.
- **Two torpedo systems.** Ships with two torpedo types fire them separately: second torpedo panel with coloured ammo (Denacity's idea), X fires the second system. Single player, co-op and multiplayer.
- **64-bit Memory Helper.** BC is 32-bit, so everything has to fit in 4 GB and big mods and HD textures run out of room. `bchost.exe` is a separate 64-bit helper that holds big data outside the game's 4 GB and hands it back when needed. Up to 2 GB by default, 3.27 GB held in testing on real Windows. Normal visible file, nothing hidden or packed. If it's missing or stops, the game carries on. On/off in Configure, usage on the Performance Overlay.
- **Multithreading.** Spare CPU cores handle ship proximity and hull damage. No more multi-second freezes: worst freeze in our 81-ship test went from 6 s to 0.04 s.
- **Preload Extended.** Big effect and ship textures load during the loading screen, so the first explosion doesn't stutter.
- **Co-op (beta).** Play one mission together. Crew picks seats in the lobby, shared targets, bridge view for crew.
- **New LCARS screens.** Configure, Quick Battle with 3D ship preview, New Game, Load Game, Multiplayer, quit dialog, loading screen, Startup and Shutdown Sequences.
- **Modern graphics.** SGSSAA, bloom, HDR, per-pixel lighting, ship shadows, colour grading, GPU ship highlights. Every effect has its own switch.
- **Texture compression.** Compressed DDS textures: video memory 5.5 GB down to 3.4 GB in our tests.
- **Performance Overlay.** FPS, frame times, every CPU core, GPU, memory and address space.

## Everything the patch does

### Display and video
- Widescreen resolutions up to 3840x2160 (sizes your display reports).
- HUD, LCARS, fonts and weapon markers fit any resolution, even after changing it in game.
- Hor+ FOV built into the exe. Our own code, hooked in at the camera sites found in AlphaYellow's FOV fix.
- Real graphics card name shown, z-buffer on for every card.
- Borderless windowed, big resolutions no longer greyed out.
- VSync option, fullscreen and windowed.
- 24-bit depth buffer, far less surface flicker.
- Menu videos fall back to the largest that fits. Bink made crash-safe in memory.
- Reworked fullscreen video: the 1080 intro, logo, credits and end movies play cleanly.
- New Skip Intro Video menu option (General, and the LCARS Display page): turn it on and the opening movies are skipped every launch. Off by default.
- Faster windowed mode and loading screens.
- Smooth motion even after days of uptime (no UptimeFaker needed).
- *More to come.*


### Controls
- 1:1 mouse, no over-rotation, no lost slow movements.
- Bridge head-look 1:1 (stock was ~7x too fast).
- Mouse wheel scrolls every menu list.
- Separate mouse speed and FOV for Tactical and Bridge.
- Bridge camera shake away from the hit side, with a switch and strength slider.
- *More to come.*


### Gameplay
- Two torpedo systems (see Highlights).
- Phasers scroll at the hardpoint's speed. Tractors use the hardpoint's colours and texture.
- Torpedo spreads home in sooner (0.5 s, was 2 s, adjustable).
- *Thanks to VonFrank for pushing these three weapons fixes.*
- Weapon hits always light the hull, even on the Borg cube.
- AI with torpedo evasion off skips the unused torpedo watcher.
- Bridge crew keep their seats after quit and reload.
- *More to come.*


### Performance
- Multithreading: 0, 1 or 2 helpers, picked for your CPU.
- Exe CPU fixes (sparse scene lists, scene-bound scanning, proximity pair removal): ~30% less main-thread work in big battles.
- Preload Extended.
- Explosions and hits reuse old slots instead of piling up: ~5% more FPS late in long fights, more near the end.
- Texture compression, DDS made by the exe on first launch with an LCARS progress window.
- Effect textures kept between missions, other textures freed when you leave one.
- 64-bit Memory Helper.
- No more GPU readback every frame: the exe skips a back-buffer lock nothing used, which through the wrapper meant a full readback twice a frame.
- Low-fragmentation heap turned on at start, so memory stays usable for longer.
- Hull damage texture cache and texture format cache.
- No menu stutter after the intro.
- *More to come.*


### Graphics
- SGSSAA anti-aliasing.
- Switchable effects: Glow Bloom, HDR Scene (FP16), Glow Shimmer Fix, Per-Pixel Lighting, Deband, Rim Light, Ship Shadows, Colour Grade, Planet Glow, Heat Ripple.
- GPU ship highlights (~7.5% faster).
- DXVK (Vulkan) set up automatically when supported.
- Effects never draw over menus or the HUD.
- Performance Overlay in four sizes, with Memory Helper rows.
- *More to come.*


### Sound
- High Quality: 64 voices, Full HRTF, 44.1 kHz.
- *More to come.*


### LCARS screens
- Configure: sliders, profiles, Mod Menus page, live previews from the Esc menu.
- Main menu top bar, New Game, Load Game, Multiplayer (plus in-game Esc page), quit dialog.
- Quick Battle that reads your install's ships and regions (no Foundation needed), with 3D preview.
- Quick Battle Spectate mode with its own camera.
- Early optional cinematic cameras: F7 Duel Cam, F8 War Correspondent. More to come.
- Glass LCARS: backlit panels, sharp fonts, calmer in-battle Configure backdrop.
- Menus react at once, nothing stock shows behind them.
- Startup Sequence ("incoming transmission") and Shutdown Sequence (powers down piece by piece).
- Loading screen with a progress bar that learns load times. Use your own picture if you like.
- Orion Delta RC4.1: Theme Selector, mutators and Wave Defense show up.
- *More to come.*


### Multiplayer
- New LCARS Multiplayer screen: Internet, LAN and Direct Connect on one page.
- Passworded games show a padlock, and only ask for a password when they need one.
- Weapon fire no longer dropped in multiplayer and co-op.
- *More to come.*


### Co-op (beta)
- Host and join from our LCARS screen, not the stock MP screens.
- Lobby with seats (crew, AI or closed). Host engages when ready.
- Join in progress, with a file check.
- Shared targeting, join/leave lines in chat.
- Bridge view for crew: switch to the bridge and stand at the Tactical station.
- Co-op Skirmish, Waves as a test mode.
- *More to come.*


### Stability and logs
- Crash guards for known stock crashes (freed objects, failed allocations, Python None, 16 MB main thread stack). Fixes for crashes on quit, changing Sound Quality and skipping the intro.
- Saving fixed (it had quietly broken). Old saves still load.
- The crash writer no longer crashes itself, so you get a real report.
- Configure > resolution > Multiplayer crash fixed.
- No crash after the intro on mods like KM.
- Finds wrappers that crash the game (dgVoodoo, ReShade) and compatibility mode, offers to move them aside.
- One log switch, logs per channel, crash log, last 5 runs kept.
- Optional 4 GB (Large Address Aware) flag.
- *More to come.*

### The patcher
- One patcher for Windows and Linux, DXVK on or off.
- Backs up what it changes. Undo restores only its own backups and puts everything back.
- Writes a receipt of what it installed.
- Every exe change checked against the stock bytes first. Nothing applied blind.

## What's to come

More is already planned, and no doubt we'll find more as we go. The aim is to get the most the engine can do and show, any way we can.

- **Volumetric effects.** Explosions, shockwaves, fires and warp with real depth. Next up. It was close to finished and should have been in this release, but lost backups and a bug set it back.
- **Download ships in game.** Browse and install from inside BC.
- **New hull damage.** Real depth on the ships. Masking is ready.
- **New suns.** Stars that behave like stars, novas included.
- **PlanetFX.** New planets, coming to the game.
- **Texture streaming.** Big textures loaded as needed, so heavy mods and HD packs fit.
- **Planet landings.** In research, with texture streaming as the groundwork.
- **Network upgrades.** Automatic port opening so hosting just works, a warning when your port is closed, the host sending missing files to players, and steadier online play in general. Started.
- **Co-op campaign.** The story missions, together.
- **More co-op on the bridge.** Crew at their stations, synced head-look and arm movement. Parked for now while the core features come first.
- **Bridge co-op for roleplay groups.** Helm, Tactical, Science, Engineering, captain gives the orders.
- **Mission scripter.** Ships, objectives, hails and story beats for your own crew.
- **More screens.** Station console on a second monitor, multi-monitor view, tablet as a station panel.
- **CameraNX.** Cinematic cameras that frame the battle like a shot from the show.
- **Steam Deck and macOS.** Coming soon.
- **VR.** The captain's chair.
- **The LCARS app.** Install, update and manage the patch and add-ons.
- **Optional mod pack.** Extras like sound upgrades.
- And a lot more.

## Thanks

**Third-party parts.** Each covers one piece, and everything else is our own exe fixes and code: **AlphaYellow** (the FOV patch sites, from their MIT-licensed FOV fix), **elishacloud** (dxwrapper, zlib, the DX7 to DX9 step), **DXVK** by Philip Rebohle and contributors (zlib, optional Vulkan).

**VonFrank.** He won't say it, so I will. He spent years on Bridge Commander: Remastered for the community and for new players. Back then BC was a crashing, buggy mess whatever mod you ran, and Remastered finally made it stable. Because of him new players came, YouTubers took an interest, and new modders, ships and ideas followed. People had ideas and talked a lot, but a domino had missed and everything stalled, leaving just talk and dead projects. He flicked the next one, and many of the engine-level projects going on now, this one included, follow from that. Thanks too for all the advice and ideas on this patch, and for pushing the weapons work: torpedoes, phasers and tractors, systems I'd never dug into. It's the least he deserves.

**Whiskers.** For letting me go on and on at him with ideas this last week or so. I stepped away from Discord and the scene for 3 years and came back bottled up with things to talk about, and he and VonFrank took the brunt of it. Sound advice, and Windows and co-op testing too. <sub>(Riker clone to be sent when technology permits.)</sub>

**BC community:** **Denacity** (Orion Delta, Bedrock, the coloured ammo idea, and advice), **Michael Wiley** (advice) <sub>(and his ship in the cutscene, if the final work meets his quality standards 😉)</sub>, **Cuddly** (the 64-voice tip), **Nocturnal**, **Morgan** (some Windows testing), **Tethys** (for getting me started on Ghidra and exe exploration, about 3 years ago), and everyone who tested, sent logs and put up with broken builds.

**The Morrowind modding community:** MGE XE, Greatness7's 64-bit helper work and OpenMW showed what an old engine can do, and they shared it openly. OpenMW alone has been built in the open since 2008, nearly 20 years of work, and MGE XE is open source too. Our Memory Helper follows the same idea.

## Problems

Run `COLLECT-LOGS.bat` (Linux: `./patch.sh logs`) and send the zip it makes.
