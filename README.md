# 🎵 ATune - Android Music Player & Streaming App

<p align="center">
  <img src="screenshots/preview.png" alt="ATune App Preview" width="300" style="border-radius: 16px;" />
</p>

<p align="center">
  <a href="https://github.com/TusharTyagi-63/ATune-App/releases/latest/download/ATune-latest.apk">
    <img src="https://img.shields.io/badge/Download-ATune%20v2.1%20APK-6366F1?style=for-the-badge&logo=android&logoColor=white" alt="Download APK" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-v2.1-blue.svg" alt="Version" />
  <img src="https://img.shields.io/badge/Platform-Android%208.0%2B-green.svg" alt="Platform" />
  <img src="https://img.shields.io/badge/Status-Stable%20Release-success.svg" alt="Status" />
  <img src="https://img.shields.io/badge/License-Free-purple.svg" alt="License" />
</p>

---

## ✨ Features & Highlights

- ⚡ **Multi-Threaded Turbo Downloads (MB/s Speeds)**: Converted single sequential streams into 4 concurrent HTTP Range segmented downloads using `RandomAccessFile` chunk streaming, bypassing CDN rate limits for ultra-fast multi-megabyte per second downloads.
- 🎤 **Robust Multi-Tier Lyrics Engine**: Exact-match Tier 0 LRCLIB (`/api/get`), safe null-resilient JSON parsing, multi-pass search fallback, and `lyrics.ovh` integration for instant, rock-solid synchronized karaoke lyrics.
- 🎚️ **Unlocked Audiophile Punch & 3D Spatial Audio**: DynamicsProcessing limiter unclamped for true physical low-end power, +12 dB sub-bass shelf with 230 Hz warmth, forced Transaural 3D virtualization for phone speakers & headphones, and self-healing session recovery.
- 🧠 **Maximized "Made For You" Discovery Graph**: 50+ Artist Affinity Knowledge Graph mapping peers across Bollywood, Punjabi, Pop, Rock, and Hip-Hop with strict 100% exclusion of already owned/liked/downloaded songs and Golden Discovery Ratio balancing.
- 🛡️ **Smooth Uninterrupted Playback**: Disabled aggressive silence-skipping and eliminated accidental tap-to-seek triggers during lyrics scrolling, ensuring songs never fast-forward or jump ahead unexpectedly.
- 🎨 **Official 3D Adaptive Branding & Material You Theming**: Modern 3D ribbon monogram and electric cyan soundwave with layered adaptive icons, sub-pixel alpha matting, and dynamic Android 13+ wallpaper theming.
- 📥 **Persistent WorkManager Background Downloads**: Crash- and reboot-resilient background download pipeline with live speed monitoring (KB/s, MB/s), pause/resume flags, and unmetered (WiFi-only) network constraint controls.
- 🔄 **Auto-Healing 403 Stream URL Refresh**: Seamlessly recovers from expired YouTube stream tokens and HTTP 403 errors, resuming playback at the exact second without skipping.
- ⚡ **Zero-Latency Next-Track Pre-Caching**: Automatically pre-buffers 2 MB of upcoming songs at 80% playback progress for seamless, instant transitions.
- 📱 **Interactive Material You Home Screen Widget**: 4x2 interactive home screen widget with dynamic accent theming, playback controls, album art, and like toggle.
- 🚗 **Android Auto & MediaBrowser Integration**: Upgraded `PlaybackService` to `MediaLibraryService` for seamless browsing and playback on Android Auto dashboards and wearable head units.
- 🎧 **Instant Music Streaming & Search**: Search millions of tracks online with instant streaming powered by Media3 ExoPlayer.
- 🔐 **Hardware-Backed AES-256 GCM Key Security**: AI Studio credentials and API keys are encrypted at rest using Android KeyStore hardware security.
- 📦 **R8 Ultra-Compact Release Packaging**: Footprint reduced down to **~4.67 MB** with resource shrinking and custom ProGuard keep rules for Media3, Room, NewPipeExtractor, and Coil.
- 🏗️ **Modular Screen Architecture**: Decoupled, dedicated Compose modules (`HomeScreen`, `SearchScreen`, `LibraryScreen`, `PlaylistDetailScreen`, `SettingsScreen`) for high maintainability and zero latency.
- 🔄 **Pull-to-Refresh Discovery**: Native swipe-down gesture support on both the Home screen and Made For You playlist to effortlessly refresh recommendations and curated mixes.
- 🤖 **Multi-Provider Conversational AI Studio**: Integrated voice assistant supporting OpenAI GPT-4o mini, Groq ultra-fast LPUs, and Google Gemini with sub-second device and playback control.
- 📊 **Interactive Taste DNA Chart**: 5-axis visual radar chart allowing you to see and fine-tune your energy, mood, and acoustic preferences interactively.
- 🎙️ **Microphone Auto-Pause & Resume**: Hardware-level recording detection automatically pauses music when external apps turn on the microphone, and smoothly resumes with a fade-in when finished.
- 📱 **Notification & Lock Screen Controls**: Control your music seamlessly with Play/Pause, Skip, Previous, and dynamic Like (❤️) & Favorite (⭐) toggles right from your notification panel and lock screen.
- 🌙 **Sleep Timer**: Built-in customizable sleep timer (preset 5/10/15/30/45/60 min or custom minutes & seconds) that gracefully closes playback.
- 📁 **Custom Playlists**: Create, manage, and organize custom playlists with persistent Room Database storage.

---

## 📲 How to Download & Install

1. **Download the APK**:
   - Click the button above or [**Direct Download ATune-latest.apk**](https://github.com/TusharTyagi-63/ATune-App/releases/latest/download/ATune-latest.apk) (always gets the latest release).
   - Alternatively, download [**ATune-v2.1.apk**](https://github.com/TusharTyagi-63/ATune-App/releases/download/v2.1/ATune-v2.1.apk).
   - Or head over to the [**Releases Tab**](https://github.com/TusharTyagi-63/ATune-App/releases) to view all versions and changelogs.

2. **Allow Installation from Unknown Sources**:
   - When opening the downloaded .apk file for the first time, Android may show a prompt: *"For your security, your phone is not allowed to install unknown apps from this source"*.
   - Tap **Settings** and toggle **"Allow from this source"**.

3. **Install & Enjoy**:
   - Tap **Install** and open **ATune** to start listening to your music!

---

## 📋 Release Information

| Attribute | Details |
|---|---|
| **App Name** | ATune |
| **Package** | com.example.atune |
| **Version** | 2.1 |
| **APK File** | ATune-v2.1.apk / ATune-latest.apk |
| **File Size** | ~4.67 MB |
| **Minimum OS** | Android 8.0 (API level 26) or higher |
| **Architecture** | Universal (ARM64, ARMv7, x86_64) |

---

<p align="center">Made with ❤️ by <a href="https://github.com/TusharTyagi-63">TusharTyagi-63</a></p>
