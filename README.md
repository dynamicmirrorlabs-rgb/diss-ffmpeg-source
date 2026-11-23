# DISS Player — FFmpeg LGPL v2.1 Compliance & Build Configuration

**Dynamic Mirror Labs** dynamically links unmodified **FFmpeg** shared libraries in **DISS Player (Dynamic Image & Spatial Sound)** for Android in compliance with the **GNU Lesser General Public License v2.1 (LGPL-2.1)**.

---

## 1. Linked & Packaged Libraries (`arm64-v8a`)
DISS Player dynamically links the following FFmpeg libraries as external `SHARED IMPORTED` `.so` libraries via Android NDK CMake:

* `libavcodec.so`
* `libavformat.so`
* `libavutil.so`
* `libswresample.so`

The v1.0 APK package also includes `libavdevice.so` and `libavfilter.so` generated from the exact same LGPL build configuration below (not actively linked by the engine). No external third-party libraries (such as `libx264`, `libx265`, `libass`, or `dav1d`) are compiled into this build.

---

## 2. License Verification (Pure LGPL v2.1)
* **License:** GNU Lesser General Public License v2.1 or later (`LICENSE` included in this repository).
* **Embedded Binary Verification (`libavutil.so`):**
  * `FFmpeg version git-2026-10-27-fa4daf6`
  * `libavutil license: LGPL version 2.1 or later`
* **GPL / Non-Free Flags:** **None.** This build does **not** use `--enable-gpl` or `--enable-nonfree`.

---

## 3. Exact Source Code
The complete, exact unmodified FFmpeg source archive used to compile the binaries shipped in **DISS Player v1.0** is hosted directly in the **[Releases](../../releases)** section of this repository (`v1.0-ffmpeg-source` — `FFmpeg-fa4daf630eb52235b1b3d0e9b1cc08392b87e9a8.zip`).

* **Upstream Version / Commit:** `git-2026-10-27-fa4daf6` (unmodified)

---

## 4. Build Environment & Exact `./configure` Command
* **Target OS / ABI:** Android `arm64-v8a` (`aarch64-linux-android26`, Min SDK 26)
* **Android NDK Version:** `27.0.12077973`
* **Host Environment:** Windows (MSYS2 / MinGW) cross-compiling with NDK LLVM Clang

```bash
./configure \
  --target-os=android \
  --arch=aarch64 \
  --cpu=armv8-a \
  --enable-neon \
  --enable-cross-compile \
  --cc=/c/Users/admin/AppData/Local/Android/Sdk/ndk/27.0.12077973/toolchains/llvm/prebuilt/windows-x86_64/bin/clang \
  --ar=/c/Users/admin/AppData/Local/Android/Sdk/ndk/27.0.12077973/toolchains/llvm/prebuilt/windows-x86_64/bin/llvm-ar \
  --ranlib=/c/Users/admin/AppData/Local/Android/Sdk/ndk/27.0.12077973/toolchains/llvm/prebuilt/windows-x86_64/bin/llvm-ranlib \
  --strip=/c/Users/admin/AppData/Local/Android/Sdk/ndk/27.0.12077973/toolchains/llvm/prebuilt/windows-x86_64/bin/llvm-strip \
  --extra-cflags='--target=aarch64-linux-android26 -O3 -ffast-math' \
  --extra-ldflags='--target=aarch64-linux-android26' \
  --prefix=./output_arm64 \
  --enable-shared \
  --disable-static \
  --disable-programs \
  --disable-doc \
  --disable-everything \
  --enable-decoder='hevc,dca,flac,aac,ac3,eac3' \
  --enable-parser='hevc,dca,flac,aac,ac3' \
  --enable-demuxer='matroska,mov,mp4,flac' \
  --enable-swresample \
  --enable-pic

make -j$(nproc)
make install
