# x2MC3DS
## A mod that aims to improve Minecraft: New Nintendo 3DS Edition's horrible performance and add some features to it.
## Features:
* 3D Support: 3D depth slider of the 3DS should work out of the box, with an additional depth slider to customize the 3D depth further (similar to what official games like Resident Evil Revelations also offer). As of right now, performance (FPS) will go roughly in half. 3D performance improvements are planned, so stay tuned for updates.

* Performance improvements: Multiple major and minor performance tweaks. Working on further improvements, stay tuned.

* Render distance slider: A simple additional slider in the graphic settings for higher render distances. This feature isn't really tested yet, but expect your FPS to drop by up to 50%, so not a great gaming experience. 3D + highest render distance is possible, but expect FPS to drop by as much as 75%. Loading additional chunks / playing for prolonged times may cause crashes (RAM on these consoles is very little).

* FPS counter: Can be turned on under Options > 3D Configuration ("Show FPS counter"). It shows up in the bottom left corner of the bottom screen, for example "95 fps T1.7 D8.1 E0.3". The three numbers show how many milliseconds each frame spends on different things:
  * T (game logic): mobs, physics, world updates.
  * D (drawing): preparing everything that gets drawn on screen.
  * E (frame end): waiting for the graphics chip and showing the finished frame.

  If you report performance issues, please include these numbers, they help a lot with finding the cause.

# Installation
## WARNING: You need a *modded NEW* Nintendo 3DS and a copy of the game, along with its latest update. If your 3DS is not already modded, follow the instructions at "https://3ds.hacks.guide/". System details of the 3DS that was used for testing are listed in the last section of this README.

* Supported version: Only the european (EUR) version of the game with the latest update (v9.11.0) is supported. Other regions or versions will not work, the patch only fits this exact version.

* Backup warning: Back up your worlds before installing, just in case. You can do this with Checkpoint (https://github.com/BernardoGiordano/Checkpoint), which is already installed if you followed 3ds.hacks.guide.

* Only one code.ips per game: Luma3DS can only load one code.ips file per game. If you already have another mod or cheat patch for Minecraft installed as a code.ips, it will be replaced by this one, and the two can't be combined.

* Step 1: Turn on game patching in Luma3DS. Hold SELECT while turning on your 3DS, enable "Enable game patching" and save.

* Step 2: Copy the code.ips file from this release to "SD:/luma/titles/000400000017CA00/code.ips" on your SD card (create the folders if they don't exist). You can do this with your PC or wirelessly with ftpd.

* Step 3: Start the game. If it was already running, close it from the HOME Menu first. The new options can be found under Options > 3D Configuration (3D depth slider and FPS counter) and in the graphic settings (render distance).

* Uninstall: Simply delete the code.ips file. Your worlds and saves are not changed by the mod.

# Optimizations
## All optimizations are listed here

* Faster matrix math: The game does a lot of matrix math (needed to position everything on screen) before every single object it draws. Its code for this was extremely inefficient, using 28 small steps for one calculation. It was replaced with a much shorter version that gives the exact same results.

* Less wasted work before drawing: Before drawing each object, the game recalculated the camera position data, did some of the calculations twice and threw the results away, and copied data around for no reason. Now it only calculates what is actually needed.

* Only send what changed: Before drawing each object, the game sent all of its graphics settings to the graphics chip again, even if nothing changed. Now only the settings that actually changed are sent.

* Skipping a useless check: Before drawing each object, the game compared a name against a list of 21 entries, one by one. For almost everything in the world (all terrain), none of them ever match, so this check is now skipped when it can't match anyway.

* Animated textures in 3D: Water, lava, fire and other animated textures were updated twice per frame in 3D mode (once for each eye), even though both eyes need the exact same result. Now they are only updated once.

* Animated textures less often: Animated textures (water, lava, fire...) used to be updated every single frame. Now they are updated every 3rd frame (around 20 times per second), which is barely noticeable but saves a lot of work.

In total, the CPU time needed to draw a frame was cut roughly in half. The first four optimizations don't change how the game looks at all.


# Performance Tests
## All of the following tests were done on a New Nintendo 3DS, with a (digital) european copy of the game.
## These numbers were measured with my own console (see Testing Setup below), so results may be different on your console.

* Overworld, Plains biome: FPS range from at least 60 up to 80, sometimes even 90 FPS while sprinting / flying through the world and actively loading new chunks. Sometimes chunk loading causes a split second hiccup, a fix is planned in the future. While standing still, FPS are mostly in the high 90's to low 100's. When running around in already loaded chunks, the FPS stay at ~80-90, until new chunks are being loaded, then it drops to ~60-70. Framerates below 60 FPS are very rare, only occurring when mining many blocks or loading new chunks.

* Underground, Caves: FPS are mostly over 90 FPS, with numbers over 100 being very common though.

* 3D Mode on: roughly half of what the FPS would be in 2D mode, +/- 15 FPS. The 3D depth slider doesn't affect performance.

* Render distance slider: Not tested yet, expect FPS numbers as low as half of the default FPS. With 3D mode turned on, expect FPS to drop by as much as 75%.

# Reporting crashes and bugs
If the game crashes or something doesn't work, please open an issue in the Issues tab of this repository. Describe what you were doing when it happened, and include the FPS counter numbers if it's a performance issue.

If the game crashes with a Luma3DS exception screen (a screen full of text and numbers):
1. Take a photo of both screens.
2. Press A to save the crash dump to your SD card, as shown on the screen.
3. Copy the dump file to your PC. It is saved in "SD:/luma/dumps/arm11/" and named like "crash_dump_00000000.dmp". You can take out the SD card and use a card reader, or copy it wirelessly with ftpd.
4. Attach the .dmp file and the photo to your issue (GitHub only accepts some file types, so you may have to put the .dmp file into a .zip first).

More about the exception screen: https://wiki.hacks.guide/wiki/3DS:Error_screens/Luma3DS_exception_screen
More about Luma3DS crash dumps: https://github.com/LumaTeam/Luma3DS/wiki/Standard-features

# Testing setup
Emulator testing was done on Azahar v2126.2. (https://azahar-emu.org/)
Console testing was done on a New Nintendo 3DS (european), with Luma3DS v13.4. (https://github.com/LumaTeam/Luma3DS)

This project was mainly developed by Claude Opus 5.5. All decompiling, testing (on an emulator) and coding was done by Claude.

# Legal
This project is not affiliated with, endorsed by or connected to Mojang Studios, Microsoft or Nintendo. Minecraft is a trademark of Mojang Studios, Nintendo 3DS is a trademark of Nintendo.

This repository and its releases only contain a patch file (code.ips) with the changes made by this mod. They do not contain any game code, assets or other copyrighted files from Minecraft. You need your own legally obtained copy of the game and its update to use this mod. Please don't ask for or share copies of the game.

Use this mod at your own risk. I'm not responsible for any damage to your console, SD card or save files.

Made by x2Clemens
MIT License
