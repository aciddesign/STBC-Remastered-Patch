# BC Unified QoL Patch

[![Windows: supported](https://img.shields.io/badge/Windows-supported-2ea44f?logo=windows&logoColor=white)](#install)
[![Linux: supported](https://img.shields.io/badge/Linux%20(Proton%2FWine)-supported-2ea44f?logo=linux&logoColor=white)](#install)
[![Steam Deck: coming soon](https://img.shields.io/badge/Steam%20Deck-coming%20soon-lightgrey?logo=steamdeck&logoColor=white)](#whats-to-come)
[![macOS: coming soon](https://img.shields.io/badge/macOS-coming%20soon-lightgrey?logo=apple&logoColor=white)](#whats-to-come)
[![Latest release](https://img.shields.io/github/v/release/aciddesign/STBC-Remastered-Patch?include_prereleases&label=latest%20release)](https://github.com/aciddesign/STBC-Remastered-Patch/releases)
[![Game: Star Trek Bridge Commander](https://img.shields.io/badge/game-Star%20Trek%3A%20Bridge%20Commander%20(2002)-blue)](#)
[![Works on stock 1.1, GOG, Remastered, Orion Delta, Legacy 1.0, Kobayashi Maru and more](https://img.shields.io/badge/works%20on-stock%201.1%20%7C%20GOG%20%7C%20Remastered%20%7C%20Orion%20Delta%20%7C%20Legacy%201.0%20%7C%20Kobayashi%20Maru%20%7C%20and%20more-blue)](#)

An unofficial fan patch for **Star Trek: Bridge Commander**. One patched `stbc.exe`, a graphics layer and a few new scripts. It only changes stock files it recognises, backs them up first, and Undo puts them back. CD, no-CD or GOG, with or without the 4 GB patch.

**Best experience: VonFrank's Bridge Commander: Remastered.** It's the recommended base and the one I build on, out of respect for what VonFrank has done for the community.

I've tinkered with BC since not long after it came out, mostly just for myself, hacking `Effects.py` and lurking. Discord got me involved, the serious work started in 2023, and Claude and Codex have helped along the way. This is the first time I've really shared any of it.

> [!WARNING]
> **THERE WILL BE BUGS.** This is a big refit of a 24-year-old engine, so things will break. When they do, please report them in **[Issues](https://github.com/aciddesign/STBC-Remastered-Patch/issues)** (logs help a lot, see [Problems](#problems)).
>
> <sub>Provided as is, with no warranty. Back up your install before patching.</sub>


## Download

> **2.47 is a BETA Preview for feedback/testing.** Everything is in testing, nothing is final. It moves to the normal Release once testers confirm it works. Best on a clean stock, or Remastered with or without Orion. I'm on Linux, so Windows testers are vital.

**[Download 2.47 BETA Preview](https://github.com/aciddesign/STBC-Remastered-Patch/releases/tag/v2.47-beta-preview)**: the patch zip, its SHA-256, What's New and the Testing focus. Previous: **[2.46 BETA Preview](https://github.com/aciddesign/STBC-Remastered-Patch/releases/tag/v2.46-beta-preview)**, **[2.45](https://github.com/aciddesign/STBC-Remastered-Patch/releases/tag/v2.45)**.
All versions: **[Releases page](https://github.com/aciddesign/STBC-Remastered-Patch/releases)**. No game files here, you need your own copy: **[Star Trek: Bridge Commander on GOG](https://www.gog.com/en/game/star_trek_bridge_commander)** (DRM-free, and the patch supports the GOG exe).

## Install

1. Unzip the patch, easiest inside the game folder next to `stbc.exe` (it asks if it can't find it).
2. Windows 10/11: run `PATCH.bat`. Nothing else to install. If Windows blocks it: right-click the zip, Properties, tick Unblock, unzip again.
3. Linux (Steam/Proton, Lutris, Wine): run `./patch.sh`.
   Tested on, and works best with, **Proton-CachyOS** (SLR build `proton-cachyos-slr-20261005`).
   Steam launch options: `WINEDLLOVERRIDES="ddraw=n,b;dsound=n,b" %command%` (dsound is for 3D Sound).
4. Remove: `UNDO.bat` (Linux: `./patch.sh undo`).

Full details, every off switch and what's been tested are in the README inside the zip.

## Highlights

- **New in 2.47: Themes.** The menus' colours now come from themes, switched live from the new **Themes tab** on the main menu (or Configure). LcarsNX, stock and your mod's own menus stay the default; a TNG theme is in as a preview, Orion Delta's own themes show up when Orion is installed, and theme packs can be dropped into the Themes folder. This is the first part: more is coming.
- **New in 2.47: a new LcarsNX main menu and a redesigned Configure** with proper dropdowns, colour schemes for LcarsNX, and opt-in Live light for the backlit panels.
- **New in 2.47: anti-aliasing modes.** SGSSAA, NVIDIA DLAA, AMD FSR 3.1, Intel XeSS, FXAA and Downsampling, picked in Configure > AA Mode on every menu type.
- **New in 2.47: widescreen by default, 3D Sound (OpenAL), co-op from any menu, a working bridge viewscreen, and backlit LCARS panels (opt-in).**
- **Multithreading (version 1).** Spare CPU cores now handle ship proximity and hull damage. This removes the multi-second proximity freezes in big battles (worst went from 6 s to 0.04 s). Smoother big battles, far fewer hitches: in our 81-ship test, hitches over 100 ms fell from 195 to 121. More threading and optimisations to come.
- **64-bit Memory Helper (version 1).** BC is 32-bit, so everything has to fit in 4 GB and big mods and HD textures run out of room. `bchost.exe` is a separate 64-bit helper that holds big data outside the game's 4 GB and hands it back when needed. Up to 2 GB by default, 3.27 GB held in testing on real Windows. Normal visible file, nothing hidden or packed. If it's missing or stops, the game carries on. On/off in Configure, usage on the Performance Overlay. More optimisations to come.
- **Torpedo lifetime from the script (2.47).** A torpedo script's GetLifetime() is honoured with no 60 s limit; torpedoes without one live 20 s.
- **Two torpedo systems.** Ships with two torpedo types fire them separately: second torpedo panel with coloured ammo (Denacity's idea), X fires the second system. Single player, co-op and multiplayer.
- **Co-op (beta).** Play one mission together. Crew picks seats in the lobby, shared targets, bridge view for crew.
- **Widescreen done right, in the exe.** Real widescreen resolutions, Hor+ FOV, HUD and fonts sized to your screen. No plugin needed. 4:3 unchanged.
- **Faster AI in big battles (really on from 2.47).** The AI's route planning reuses answers it already has and skips collision checks between ships that can't meet. Worst late-battle stall went from 1,149 ms to 37 ms in our 81-ship test.
- **Preload Extended.** Big effect and ship textures load during the loading screen, so the first explosion doesn't stutter.
- **New LCARS screens.** Configure, Quick Battle with 3D ship preview, New Game, Load Game, Multiplayer, quit dialog, loading screen, Startup and Shutdown Sequences.
- **Driver-free SGSSAA.** True sparse grid supersampling built into the game through our own d3d9 layer. Any GPU, Windows and Linux, no NVIDIA driver tricks. The first game we know of with SGSSAA built in like this.
- **Graphics.** Bloom, HDR, per-pixel lighting, ship shadows, colour grading, GPU ship highlights. Every effect has its own switch.
- **Texture compression.** Compressed DDS textures: video memory 6.6 GB down to 2.8 GB in our tests.
- **Performance Overlay.** FPS, frame times, every CPU core, GPU, memory and address space.

## Bug fixes in 2.47 (fixed, please test)

- **Faint whine on some sounds and music**: sound output back to stock 22050 Hz (Windows and Linux); a rate you set yourself is kept. Thanks **VonFrank42**.
- **SunNX: ships drawing through each other when the sun is on screen, jagged sun edge.** Thanks **VonFrank42**.
- **A dark disc flickering on moons seen through the bridge viewscreen.** Thanks **VonFrank42**.
- **VonFrank's menus: the LCARS theme can now be picked, and his own intro still plays in fullscreen.** Thanks **VonFrank42**.
- **Second torpedo system: power use and the Weapons power slider now count both systems.**
- **Orion / Bedrock: Quick Battle lists the ships inside class sub-menus** (pick, add and fly them). Thanks **Denacity**.
- **KM (Kobayashi Maru): no more crash from JaggieFix on startup.**
- **Crash on quitting after loading a campaign save**; old saves load safely. Saving and loading now skip a broken object instead of crashing (logged to saveload-fix.log).
- **Field of view stuck after changing resolution** (an old stock bug).
- **Co-op needed the LCARS menu**: it opens from any menu now.
- **Configure options missing on Classic / stock / Orion / KM menus**: the effect sliders, PlanetNX / SunNX and AA Mode are under Configure > Graphics.
- **Lower-end graphics without DXVK: texture preloading is off by default**, which stops a crash from running out of memory at high AA.
- **The log's first line said version 2.11**; it shows 2.47 now. Thanks **VonFrank42**, **Daimo** and **Alex400ZZ** for the logs.
- **Themes tab: long lists scroll, and the drawer opens above the Performance Overlay.**
- **AI speed-up (since 2.44) was never switched on** for players; it is on now.
- **Quick Battle drag and drop** is back.
- Still to confirm from 2.46: the display auto-fix for old or modded setups (thanks **ACR2023**, **Morgan**, **Alex400ZZ**), less stutter at mission start.

Please also check: Linux without DXVK / native d3d9: texture preload stays off by design (it should run as stock there).

Tell me in **[Issues](https://github.com/aciddesign/STBC-Remastered-Patch/issues)** if any of them still happen.

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
- Widescreen is the default: new installs start at your desktop size (16:9 or wider); old 640x480 / 800x600 / 1024x768 setups move to it.
- The view widens / narrows at once when you change resolution in game.
- HUD Scale, Menu Scale and HUD Width in Configure.
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
- The Esc menu cursor keeps its spot.
- Mouse wheel sets ship speed outside menus.
- **Controller support (early version):** Xbox-style (XInput) pads and mouse buttons 4 / 5 bindable in Configure > Controls, LB / RB layers for extra binds, default pad bindings. On by default.
  - It's in and usable now, but this is an EARLY version. What's coming:
    - **Next:** the game will support pads properly, with a strong set of default bindings and new UI made for the pad (hold a button for a quick radial menu, menus and screens you can drive with the pad), so it plays like a pad-optimised game for those who want it.
    - **After that:** HOTAS / joystick support.
  - Updated in this build: the Controls page shows Xbox button names, turn and roll keep their keyboard keys with a pad plugged in, and pad binds you hold down no longer come back as an empty key after a restart.
  - Problems? Set `[ControllerNX] Enabled|0` in options.cfg to turn it off.
- *More to come.*


### Gameplay
- Two torpedo systems (see Highlights). The second system draws its own power and follows the Weapons slider.
- Phasers scroll at the hardpoint's speed. Tractors use the hardpoint's colours and texture. (Thanks VonFrank for reporting both.)
- Torpedo spreads home in sooner (0.5 s, was 2 s, adjustable).
- *Thanks to VonFrank for pushing these three weapons fixes.*
- Weapon hits always light the hull, even on the Borg cube.
- AI with torpedo evasion off skips the unused torpedo watcher.
- Bridge crew keep their seats after quit and reload.
- *More to come.*


### Performance
- Multithreading v1: 0, 1 or 2 helpers, picked for your CPU.
- Exe CPU fixes (sparse scene lists, scene-bound scanning, proximity pair removal): ~30% less main-thread work in big battles.
- Preload Extended.
- AI route-planning cache and collision-check skip (each half can be turned off by deleting `aipathcache.mode` or `aiskip.mode`).
- Explosions and hits reuse old slots instead of piling up: ~5% more FPS late in long fights, more near the end.
- Texture compression, DDS made by the exe on first launch with an LCARS progress window.
- Effect textures kept between missions, other textures freed when you leave one.
- 64-bit Memory Helper v1.
- No more GPU readback every frame: the exe skips a back-buffer lock nothing used, which through the wrapper meant a full readback twice a frame.
- Low-fragmentation heap turned on at start, so memory stays usable for longer.
- Hull damage texture cache and texture format cache.
- No menu stutter after the intro.
- Stock memory leak between missions fixed. Old ships are no longer kept after a mission ends, so long sessions use far less memory (1.1 GB down to 0.47 GB in our test).
- *More to come.*


### Graphics
- Anti-aliasing modes (Configure > AA Mode): SGSSAA, NVIDIA DLAA, AMD FSR 3.1 native AA, Intel XeSS native AA, FXAA, plus Downsampling 1.5x / 2x. 3D scene only, menus untouched.
- PlanetNX and SunNX: new planets (atmosphere, clouds, city lights) and an animated sun with an HD lens flare.
- ViewscreenNX: the bridge viewscreen picture sits flat at every head angle; the targeting box follows the ship to the edge.
- Effects look the same with AA on or off; graphics settings live in options.cfg under their own headings.
- Backlit LCARS panels (Gel, Smoked, Filmed): opt-in, Off by default, in the Themes tab.
- Switchable effects: Glow Bloom, HDR Scene (FP16), Glow Shimmer Fix, Per-Pixel Lighting, Deband, Rim Light, Ship Shadows, Colour Grade, Planet Glow, Heat Ripple.
- GPU ship highlights (~7.5% faster).
- DXVK (Vulkan) set up automatically when supported.
- Effects never draw over menus or the HUD.
- Performance Overlay in four sizes, with Memory Helper rows.
- Ship glow maps work with Per-Pixel Lighting.
- Under DXVK: 1 queued frame for lower input lag, and 16x anisotropic filtering for sharper textures.
- *More to come.*


### Sound
- High Quality: 64 voices, Full HRTF (stock 22050 Hz output, no whine).
- 3D Sound (OpenAL): DSOAL + OpenAL Soft, with Headphones / Speakers / 5.1 / 7.1 and HRTF. Off until you pick it.
- *More to come.*


### LCARS screens
- Configure: sliders, profiles, Mod Menus page, live previews from the Esc menu.
- On/off switches in Configure > Graphics for Multithreading, Memory Helper and Two Torpedo Systems. Turning torpedoes off brings back the stock weapons panel from the next mission.
- Themes: Classic (the stock look), LcarsNX and colour scheme packs (TNG 2357 / 2369 / 2375, LCARS Picard / Nemesis), sharp at any resolution, switched live from the Themes tab on the main menu or Configure. Your existing menus stay the default.
- Classic, stock and mod menus get the graphics sliders and AA Mode under Configure > Graphics.
- Configure profile bar: Save / Load / Defaults. LcarsNX Configure uses proper dropdowns, with Colour Scheme and Live light under General.
- Main menu top bar, New Game, Load Game, Multiplayer (plus in-game Esc page), quit dialog.
- Quick Battle that reads your install's ships and regions (no Foundation needed), with 3D ship and bridge previews and drag and drop into the teams.
- Quick Battle Spectate mode with its own camera.
- Early optional cinematic cameras: F7 Duel Cam, F8 War Correspondent. More to come.
- Glass LCARS: backlit panels, sharp fonts, calmer in-battle Configure backdrop.
- Menus react at once, nothing stock shows behind them.
- Startup Sequence ("incoming transmission") and Shutdown Sequence (powers down piece by piece).
- Loading screen with a progress bar that learns load times. Use your own picture if you like.
- Orion Delta RC4.1: Theme Selector, mutators and Wave Defense show up.
- Configure > Display rebuilt: windowed/fullscreen switch and dropdowns, in game.
- *More to come.*


### Multiplayer
- New LCARS Multiplayer screen: Internet, LAN and Direct Connect on one page.
- Passworded games show a padlock, and only ask for a password when they need one.
- Weapon fire no longer dropped in multiplayer and co-op.
- *More to come.*


### Co-op (beta)
- Opens from any menu theme (Classic, LCARS, mod menus).
- Host and join from our LCARS screen, not the stock MP screens.
- Lobby with seats (crew, AI or closed). Host engages when ready.
- Join in progress.
- Shared targeting, join/leave lines in chat.
- Recent addresses are remembered across restarts.
- Bridge view for crew: switch to the bridge and stand at the Tactical station.
- Co-op Skirmish, Waves as a test mode.
- *More to come.*


### Stability and logs
- Crash guards for known stock crashes (freed objects, failed allocations, Python None, 16 MB main thread stack). Fixes for crashes on quit, changing Sound Quality and skipping the intro.
- Saving fixed (it had quietly broken). Old saves still load.
- No crash when you quit after loading a campaign save; saving and loading skip a broken object instead of crashing.
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
- Script fixes only go over stock files. A mod's own version is left alone.
- Checks for Vulkan first, and leaves DXVK out with a warning if your PC can't run it (no black screen).
- It talks like the Enterprise computer: "Working.", "Please confirm.", "Unable to comply.", "Program complete."

## Coming next: a new UI system (for theme makers)
The menus are moving to a new UI layer built on RmlUi, an HTML / CSS-style UI kit, drawn by our own renderer inside the game. It's being tested now and isn't in this build.
- **Themes become files you can edit:** layouts in markup, looks in stylesheets. Make a full theme, or just a colour scheme for an existing one.
- **Lots of options:** your own layouts, fonts and colours; animations and transitions; gradients; blur, glow and drop-shadow filters; vector (SVG) art.
- **After Effects animations:** animated pieces made in Adobe After Effects and exported as Lottie files can play in a theme.
- **Sharp at any resolution**, with live reload while you edit, so you see changes straight away.
- **Drop-in theme folders** that the Themes tab lists, and later a small theme-maker app to build, export and share themes.
- Today's colour-scheme packs (theme.cfg) keep working.

## What's to come

More is already planned, and no doubt we'll find more as we go. The aim is to get the most the engine can do and show, any way we can.

- **Volumetric effects.** Explosions, shockwaves, fires and warp with real depth. Next up. It was close to finished and should have been in this release, but lost backups and a bug set it back.
- **Fire groups.** Put your weapons into groups, with a 4th fire key. Denacity's idea.
- **Wreck and debris limit.** Keeps the wreckage in check, with a vaporize effect for old wrecks and an Auto mode.
- **Download ships in game.** Browse and install from inside BC.
- **Ship damage.** Hull damage with real depth on the ships. In development for a while now, with its own demo tool, and the masking of the right areas is already done. It ships when it meets our quality bar.
- **Improved collisions.** A more realistic collision rework, built on the damage and break-up system. Parked for now.
- **New suns.** Stars that behave like stars, novas included.
- **PlanetFX.** New planets, coming to the game.
- **Texture streaming.** Big textures loaded as needed, so heavy mods and HD packs fit.
- **Planet landings.** In research, with texture streaming as the groundwork.
- **New loading screens.** Bigger plans for these. Then again, with texture streaming, who needs loading screens? 😉
- **Network upgrades.** Automatic port opening (UPnP), so you won't have to set up port forwarding yourself. Until then, hosts still need to forward the game port. Also planned: a warning when your port is closed, the host sending missing files to players, and steadier online play in general.
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

**Totally Games.** For making Bridge Commander in the first place. Over twenty years on, people are still flying it, modding it and finding new ways to sit in the captain's chair. None of this exists without the game they built.

**Third-party parts.** Each covers one piece, and everything else is our own exe fixes and code: **AlphaYellow** (the FOV patch sites, from their MIT-licensed FOV fix), **elishacloud** (dxwrapper, zlib, the DX7 to DX9 step), **Antonio** font by Vernon Adams (SIL Open Font License, for the LCARS text), **DXVK** by Philip Rebohle and contributors (zlib, optional Vulkan), **DSOAL and OpenAL Soft** by Chris Robinson (kcat) (LGPL, 3D Sound), **NVIDIA DLSS** (DLAA), **AMD FidelityFX FSR 3.1** (MIT), **Intel(R) Xe Super Sampling (XeSS) SDK: Copyright (C) 2025 Intel Corporation**, **FXAA 3.11** by Timothy Lottes / NVIDIA.

**VonFrank.** He won't say it, so I will. He spent years on Bridge Commander: Remastered for the community and for new players. Back then BC was a crashing, buggy mess whatever mod you ran, and Remastered finally made it stable. Because of him new players came, YouTubers took an interest, and new modders, ships and ideas followed. People had ideas and talked a lot, but a domino had missed and everything stalled, leaving just talk and dead projects. He flicked the next one, and many of the engine-level projects going on now, this one included, follow from that. Thanks too for all the advice and ideas on this patch, and for pushing the weapons work: torpedoes, phasers and tractors, systems I'd never dug into. It's the least he deserves.

**Whiskers.** For letting me go on and on at him with ideas this last week or so. I stepped away from Discord and the scene for 3 years and came back bottled up with things to talk about, and he and VonFrank took the brunt of it. Sound advice, and Windows and co-op testing too. <sub>(Riker clone to be sent when technology permits.)</sub>

**BC community:** **Denacity** (Orion Delta, Bedrock, the coloured ammo and fire group ideas, and advice), **Michael Wiley** (advice), **Cuddly** (the 64-voice tip), **Morgan** (some Windows testing), **Tethys** (for getting me started on Ghidra and exe exploration, about 3 years ago), and everyone who tested, sent logs and put up with broken builds.

**Mark.** For his advice on licences. If you love BC, check out his project, **[Dauntless](https://bc-dauntless.netlify.app/)**, an open reimplementation of the BC engine.

**Nocturnal.** Keep an eye on his Unreal Engine project too (link coming soon).

**Also:** **Michael Okuda**, whose LCARS design language the screens follow. And the tools that made the exe work possible: **Ghidra** and **pycdc**.

**The Morrowind modding community:** MGE XE, Greatness7's 64-bit helper work and OpenMW showed what an old engine can do, and they shared it openly. OpenMW alone has been built in the open since 2008, nearly 20 years of work, and MGE XE is open source too. Our Memory Helper follows the same idea.

## Problems

Run `COLLECT-LOGS.bat` (Linux: `./patch.sh logs`), then send the zip it makes with a short note on what happened. Open an issue in **[Issues](../../issues)** here.

Controller causing trouble? Close the game and set `[ControllerNX] Enabled|0` in options.cfg.

---

<sub>Star Trek: Bridge Commander was made by Totally Games and published by Activision. Star Trek belongs to CBS Studios / Paramount. This is a fan project and isn't made or endorsed by any of them.</sub>
