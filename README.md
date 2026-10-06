# Galify - source code for its LGPL libraries

Galify is an offline photo, video and music gallery for Android, distributed on Google Play.
Galify itself is proprietary. Its native library `libffmpegJNI.so` statically links three
libraries licensed under the **GNU Lesser General Public License, version 2.1**:

| Library | Version | Licence |
|---|---|---|
| [FFmpeg](https://ffmpeg.org) (libavcodec, libavformat, libavutil, libswresample, libswscale) | 9.0.2 with 7 patches | LGPL-2.1-or-later (built without `--enable-gpl`, `--enable-version3`, `--enable-nonfree`) |
| [LibRaw](https://www.libraw.org) | 0.21.3 | LGPL-2.1 (chosen from its LGPL-2.1 / CDDL-1.0 dual licence) |
| [codec2](https://github.com/drowe67/codec2) | 1.2.0 + 108 commits (310777b) | LGPL-2.1 |

As LGPL-2.1 (sections 4 and 6) requires, this repository provides, for every Galify version
that ships them:

* the **complete corresponding source code** of these libraries, exactly as built, with the
  patches, compatibility files and build script used to build them;
* the **relinking materials**: Galify's own object files, every static library and the exact
  link command, so you can rebuild `libffmpegJNI.so` with a modified version of any of these
  libraries and use it in Galify.

## Downloads

Each Galify version has a release here with one zip file. The release notes give its SHA-256.

| Galify version | Release | File |
|---|---|---|
| 1.0.0 (build 1) | [galify-1.0.0-build1](https://github.com/muhammad-ahsan-m/galify-lgpl-sources/releases/tag/galify-1.0.0-build1) | `galify-1.0.0-build1-lgpl.zip` |

Inside the zip, `README.txt` explains the layout and the relinking steps:

* `source/` - FFmpeg 9.0.2 (official tarball), LibRaw 0.21.3 (official tarball), codec2 at commit
  310777b, and `galify-native-build/` (FFmpeg patches, compatibility files, `build_ffmpeg.sh`,
  `fetch_sources.sh`, and `FFMPEG_NOTICE.md` with the exact configuration).
* `relink/<abi>/` (arm64-v8a, armeabi-v7a, x86_64) - `obj/` (Galify's object files), `lib/` (all
  static libraries) and `link.sh`. Relinking the unmodified kit reproduces the shipped
  `libffmpegJNI.so` byte for byte; `binaries.txt` lists the checksums.
* `notices/` - the licence texts Galify shows under Settings > About > Open source licences.

## Your rights

You may modify these libraries and relink them into Galify for your own use, and
reverse-engineer Galify to the extent needed to debug such modifications. To use a modified
library: rebuild it, replace the matching archive in `relink/<abi>/lib/`, run
`NDK=/path/to/android-ndk-r27 relink/<abi>/link.sh`, put the resulting `libffmpegJNI.so` into the
APK's `lib/<abi>/`, re-sign the APK with your own key and install it (uninstall the Play version
first, since the signature differs).

## Written offer

These materials stay available here for at least three years after the corresponding Galify
version was last distributed. For the same period, anyone who received that version of Galify
may also request them from **m.ahsanmobarki@gmail.com** and will receive them for no more than
the cost of providing them.

This repository contains no other part of Galify's source code.
