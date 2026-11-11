# Galify - source code for its LGPL libraries

Galify is an offline photo, video and music gallery for Android. Galify itself is proprietary.
Its native library `libffmpegJNI.so` statically links three libraries licensed under the **GNU
Lesser General Public License, version 2.1**:

| Library | Version | Licence |
|---|---|---|
| [FFmpeg](https://ffmpeg.org) (libavcodec, libavformat, libavutil, libswresample, libswscale) | 9.0.2 with 7 patches | LGPL-2.1-or-later (built without `--enable-gpl`, `--enable-version3`, `--enable-nonfree`) |
| [LibRaw](https://www.libraw.org) | 0.21.3 | LGPL-2.1 (chosen from its LGPL-2.1 / CDDL-1.0 dual licence) |
| [codec2](https://github.com/drowe67/codec2) | 1.2.0 + 108 commits (310777b) | LGPL-2.1 |

As LGPL-2.1 (sections 4 and 6) requires, this repository provides, for every Galify build that
ships them:

* the **complete corresponding source code** of these libraries, exactly as built, with the
  patches, compatibility files and build script used to build them;
* the **relinking materials**: Galify's own object files, every static library and the exact
  link command, so you can rebuild `libffmpegJNI.so` with a modified version of any of these
  libraries and use it in Galify.

This is the one permanent repository for all of Galify's LGPL packages. Packages are only ever
added; none is replaced or removed while its availability period lasts.

## Release history and downloads

Each package belongs to one **native build** of Galify, named after the first eight hex digits
of the arm64-v8a `libffmpegJNI.so` SHA-256 it rebuilds. The native build, not the app version,
identifies a package: two builds can share an app version, and several app versions can share
one native build.

| Native build | App version (versionCode) | Distribution | Release | File | Published | Availability |
|---|---|---|---|---|---|---|
| **b2b70aff** | 1.0.0 (1) | **Google Play** | [galify-1.0.0-build1-lib-b2b70aff](https://github.com/muhammad-ahsan-m/galify-lgpl-sources/releases/tag/galify-1.0.0-build1-lib-b2b70aff) | `galify-1.0.0-build1-lib-b2b70aff-lgpl.zip` | 2026-11-11 | Available; at least 3 years after this build was last distributed |
| 96d9f764 | 1.0.0 (1) | Earlier build of 7 October 2026 | [galify-1.0.0-build1](https://github.com/muhammad-ahsan-m/galify-lgpl-sources/releases/tag/galify-1.0.0-build1) | `galify-1.0.0-build1-lgpl.zip` | 2026-10-07 | Available; at least 3 years after this build was last distributed |

### Native build b2b70aff - Galify 1.0.0 (versionCode 1), Google Play

* Release: [galify-1.0.0-build1-lib-b2b70aff](https://github.com/muhammad-ahsan-m/galify-lgpl-sources/releases/tag/galify-1.0.0-build1-lib-b2b70aff)
* File: `galify-1.0.0-build1-lib-b2b70aff-lgpl.zip` (71,148,349 bytes)
* File SHA-256: `8654b0edaaa97e8496f993a7f91ac79d041c09e6439a7b2a80a1d3ec02550940`
* `libffmpegJNI.so` SHA-256:
  * arm64-v8a: `b2b70aff5fdda7bf102689d95cfeef4c21167f598c83e513d08664bdeb8949c9`
  * armeabi-v7a: `6a4c9a68c0bdd571b0482f0072dd26122733207120ff3f6e5824098ebf9a5899`
  * x86_64: `c34ce3bd03710a6c02730d9cbe047765f3917447ee30576b1b6eced7c34bb893`
* Published 2026-11-11.

### Native build 96d9f764 - Galify 1.0.0 (versionCode 1), build of 7 October 2026

* Release: [galify-1.0.0-build1](https://github.com/muhammad-ahsan-m/galify-lgpl-sources/releases/tag/galify-1.0.0-build1)
* File: `galify-1.0.0-build1-lgpl.zip` (71,141,832 bytes)
* File SHA-256: `1dc8c31d866ef9d3d019de5549442804727fe4d9627a4a550ea257774f6662b8`
* `libffmpegJNI.so` SHA-256:
  * arm64-v8a: `96d9f764c7a701e15d353cdd0a6246eaac51b8346d1bc2f40b89ea8590fc2c6b`
  * armeabi-v7a: `b6d59214d6e98b641e5d97ee543a577d68f5e725ebf474e96f018f84655ef538`
  * x86_64: `b0f59923461165bdbac341e15b6b9947af0cea4624a9cacdaaaebf0c64b2404a`
* Published 2026-10-07. Its release notes originally gave the checksum `2eceefc8…`, which
  belongs to another copy of the package kept by the developer (same sources and relinking kit, a
  `binaries.txt` naming a different APK/AAB). The notes were corrected on 2026-11-11; the tag and
  the attached file were not changed.

The exact APK and AAB each package belongs to are listed in that package's `binaries.txt`.

## Which package is mine?

1. If you installed **Galify 1.0.0 (versionCode 1) from Google Play**, use native build
   **b2b70aff**.
2. To check any installation: on a computer with `adb`, run
   `adb shell pm path com.ahsansoftware.galify`, pull the APK for your device's ABI (a Play
   install lists a `split_config.<abi>.apk`), and compute the SHA-256 of its
   `lib/<abi>/libffmpegJNI.so`. The release whose hash for that ABI matches is your package.
3. Galify shows its app version under Settings > About. The versionCode is shown by
   `adb shell dumpsys package com.ahsansoftware.galify | grep version`.

## App updates and native builds

Galify updates do not always change the LGPL libraries:

* **An update that changes only Galify's Dart code, user interface, icons or other assets**
  leaves `libffmpegJNI.so` byte-identical. The existing package still applies to it, and no new
  archive is published; the table above is updated to list the new app version against the
  native build it ships.
* **An update that changes the native libraries** (FFmpeg, LibRaw, codec2, their patches or
  configuration, Galify's JNI code, the NDK or the link) produces a new `libffmpegJNI.so`, and so
  a new native build ID, a new release and a new archive.

Older packages always stay available for the builds they correspond to.

## What each zip contains

Inside each zip, `README.txt` explains the layout and the relinking steps:

* `source/` - FFmpeg 9.0.2 (official tarball), LibRaw 0.21.3 (official tarball), codec2 at commit
  310777b, and `galify-native-build/` (FFmpeg patches, compatibility files, `build_ffmpeg.sh`,
  `fetch_sources.sh`, and `FFMPEG_NOTICE.md` with the exact configuration).
* `relink/<abi>/` (arm64-v8a, armeabi-v7a, x86_64) - `obj/` (Galify's object files), `lib/` (all
  static libraries) and `link.sh`. Relinking the unmodified kit reproduces that build's
  `libffmpegJNI.so` byte for byte; `binaries.txt` lists the checksums.
* `notices/` - the licence texts Galify shows under Settings > About > Open source licences.
* `MANIFEST.sha256` - the checksum of every file in the package.

**Build paths:** the object files, static libraries and the shipped `libffmpegJNI.so` contain
the directory paths of the machine they were built on (in debug and source-file information
recorded by the compiler). They are kept unchanged, because removing them would change the
binaries and break the byte-for-byte match between the kit and the shipped library. They have no
effect on relinking.

## Your rights

You may modify these libraries and relink them into Galify for your own use, and
reverse-engineer Galify to the extent needed to debug such modifications.

To use a modified library:

1. Rebuild it, and replace the matching archive in `relink/<abi>/lib/`.
2. Run `NDK=/path/to/android-ndk-r27 relink/<abi>/link.sh`.
3. Put the resulting `libffmpegJNI.so` into the APK's `lib/<abi>/`. A Google Play install is a
   set of APKs, and the library is in `split_config.<abi>.apk`.
4. Re-sign every APK of the set with your own key and install them together
   (`adb install-multiple`).

Android installs a differently signed copy only after the original is uninstalled, and
uninstalling deletes Galify's data. That includes the private gallery, whose files cannot be
recovered without that installation's key, so export anything you want to keep first.

## Availability and written offer

**Each package listed above stays available here for at least three years after the Galify build
it corresponds to was last distributed.** The period runs separately for each build: publishing a
newer package never removes or shortens the availability of an older one, and no release is
deleted while its period lasts.

For the same period, anyone who received a Galify build may also request that build's materials
from **m.ahsanmobarki@gmail.com** and will receive them for no more than the cost of providing
them.

This repository contains no other part of Galify's source code.
