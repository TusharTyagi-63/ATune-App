# 🎵 ATune - Android Music Player & Streaming App

<p align="center">
  <img src="screenshots/preview.png" alt="ATune App Preview" width="300" style="border-radius: 16px;" />
</p>

<p align="center">
  <a href="https://github.com/TusharTyagi-63/ATune-App/releases/latest/download/ATune-latest.apk">
    <img src="https://img.shields.io/badge/Download-ATune%20v3.5%20APK-6366F1?style=for-the-badge&logo=android&logoColor=white" alt="Download APK" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-v3.5-blue.svg" alt="Version" />
  <img src="https://img.shields.io/badge/Platform-Android%208.0%2B-green.svg" alt="Platform" />
  <img src="https://img.shields.io/badge/Status-Stable%20Release-success.svg" alt="Status" />
  <img src="https://img.shields.io/badge/License-Free-purple.svg" alt="License" />
</p>

---

## ✨ Features & Highlights

- 🧠 **ML Best Practices & Intelligence Hardening (v3.4)**:
  - 🛡️ **Bounded Live Centroid EMA**: Live playback feedback updates now use an Exponential Moving Average ($\alpha=0.15$) with a strict $L_2$ norm cap ($\le 10.0$), mathematically preventing feedback loop divergence and runaway centroid drift over long listening sessions.
  - 🔒 **Negative Hash Guard**: Guarded all vector slot indexing with bitwise masking (`slot = 24 + ((hash and 0x7FFFFFFF) % 8)`), eliminating negative modulo corruption from `abs(Int.MIN_VALUE)`.
  - 🪄 **Semantic Vector Purity**: Decontaminated prompt vector embeddings by removing raw text hashing into artist slots, ensuring natural language mood prompts (e.g., "chill lofi study beats") project only into acoustic dimensions without spurious artist bias.
  - 🎯 **Contextual Bandit (LinUCB) Covariance**: Formalized upper confidence bound exploration with true feature context covariance ($\alpha \sqrt{x^T A^{-1} x}$), maintaining optimal exploration/exploitation balance.
  - ⏳ **Softened Negative Penalties with Half-Life Decay**: Negative artist penalties now decay smoothly with exponential half-life ($T_{half}=14\text{d}$ for feedback, $6\text{h}$ for live fast skips), eliminating recommendation echo chambers.

- 🎛️ **Audio DSP & Hardware Equalizer Interpolation (v3.4)**:
  - 📐 **Piecewise Log-Frequency Hardware EQ Interpolation**: Automatically maps the 5 Harman target reference anchors (60 Hz, 230 Hz, 1 kHz, 4 kHz, 14 kHz) across 5-, 6-, 8-, and 10-band hardware equalizers based on each device's actual center frequencies (`eq.getCenterFreq()`).
  - ➕ **Additive Composite Equalizers**: Users can now adjust personal EQ sliders on top of AutoEq headphone compensation curves ($g_{composite} = g_{auto} + g_{user} - 0.5f$).
  - 🎚️ **Orthogonal Volume Envelopes**: Re-architected volume management into independent envelopes ($V_{effective} = V_{fade} \times V_{duck}$), eliminating volume race conditions between crossfading and voice assistant speech ducking.

- 🗄️ **Room Database Schema Safety & Migration Resilience (v3.4)**:
  - 🛡️ **Legacy Upgrade Paths**: Added explicit migration paths from legacy version 2 (`MIGRATION_2_6`, `MIGRATION_2_8`) and `fallbackToDestructiveMigrationOnDowngrade()`, eliminating startup crashes for users upgrading from older versions.
  - ⚡ **O(log N) Indexed Feedback Queries**: Added composite indices on `(feedbackType, timestamp)` in `SongFeedbackEntity`.

- 🎙️ **Voice Assistant Concurrency & Context Safety (v3.4)**:
  - 🚀 **Zero-Hang Speech Recognition**: Pre-cancelling active sessions before `startListening()` eliminates `ERROR_RECOGNIZER_BUSY` (code 8) on rapid voice button presses.
  - 🧹 **Activity Leak Prevention**: Ensured `applicationContext` is used throughout `TextToSpeech` and recognizer initializations.

- 📱 **Complete Home Screen Offline Caching (v3.4)**:
  - 💾 **Full Shelf Offline Serialization**: Extended `HomeScreenData` to serialize Decade (60s, 70s, 80s, 90s) and Workout playlists for instant 0ms offline startup across the entire Home screen.

- ⚡ **Spotify-Grade Ultra-Low Network Streaming Engine (v3.3)**:
  - 🌐 **Dynamic Adaptive Streaming ("Auto")**: Real-time `NetworkQualityMonitor` detects connection speed and metered states. On 2G, EDGE, 3G, or congested cellular connections, automatically negotiates crystal-clear Opus 50–70 kbps audio (`itag 249` & `250`), reducing data consumption by 70–80% (requiring only ~6–8 KB/s) so playback never stalls or stutters.
  - 🏎️ **Ultra-Fast 800ms Playback Start**: Re-engineered ExoPlayer load control starts streaming in under 800ms of audio buffering instead of demanding 15–20 seconds, delivering instant playback even on weak cellular connections.
  - 🛡️ **Deep 180s (3-Minute) Resilient Buffer**: Look-ahead buffer expands up to 3 full minutes when bandwidth is available, absorbing subway tunnels, elevators, and cell tower handovers seamlessly.
  - 💾 **Instant Zero-Latency Cache-First Playback**: Any previously played or pre-cached track starts playing immediately in < 5ms directly from local disk cache, requiring zero network calls or NewPipe extractions.
  - 📱 **Offline-First Home Screen Caching**: All home categories (Trending, Bollywood, Punjabi, Haryanvi, Bhojpuri, International, and Made For You) are stored in persistent disk cache, rendering the complete home screen in 0ms on app open without empty spinners or network timeout errors.
  - 🖼️ **90% Lighter Thumbnails on Low Network / Data Saver**: Dynamically switches thumbnail resolution from heavy 200 KB `hq720.jpg` to crisp 8–12 KB `mqdefault.jpg`, saving 95% of image bandwidth and keeping all cellular bandwidth dedicated to audio.
  - 🎚️ **Dedicated "Low Network & Data Saver" Mode**: Toggleable with one tap in Settings to lock the entire app into maximum data savings and stutter-free low-bandwidth operation.
  - 🔄 **NewPipe Persistent HTTP Cache & Warm Connection Pooling**: 40 MB disk cache and OkHttp connection pooling to prevent repeated network handshakes on mobile data.

- 🧠 **On-Device ML & Intelligent Audio Systems (v3.2)**:
  - 🤖 **Taste Autopilot & Live Playback Telemetry**: Automatically learns your taste as you listen. Completing $\ge 70\%$ of a song boosts artist affinity and shifts the positive taste centroid; skipping within 20 seconds registers a gentle penalty without requiring manual button presses.
  - 🎤 **Instant AI Vocal Attenuation / Karaoke Engine**: One-tap vocal suppression right from the player sheet! Implements a real-time center-channel notch filter attenuating human vocal formants (250 Hz – 3.5 kHz) by -12 dB to -15 dB while preserving bass punch and high-frequency sparkle.
  - 🎧 **Dynamic AI AutoEq Headphone Compensation**: Automatically detects connected hardware (Apple AirPods, Sony WH/WF-1000XM, Samsung Galaxy Buds, Bose QC, Sennheiser, Pixel Buds) via `AudioManager` and applies proven Harman Target parametric curves for acoustic correction.
  - 🎚️ **Harmonic Equal-Power DJ Crossfader**: Mathematical constant-power trigonometric crossfading ($\cos(\frac{\pi t}{2})$ and $\sin(\frac{\pi t}{2})$) ensuring the perceived volume never dips between transitioning tracks.
  - 🪄 **Smart Prompt / Mood Playlist Builder**: Natural language semantic parser synthesizing 32-dimensional target vectors and ranking tracks by cosine similarity, with quick-tap AI Mood chips (Gym Beast Mode, Late Night Drive, Rainy Lo-Fi, Acoustic Coffeehouse) in Search.

- 📜 **Unlimited Playlist Importing & Custom Management (v3.2)**:
  - ♾️ **Zero Song Import Limit**: Multi-page pagination loop extracting up to 50 pages (~2,500 tracks) from YouTube and public Spotify playlists, completely eliminating the previous 50-song cap.
  - 🛠️ **Full Playlist Editing & Customization**: All imported playlists can now be renamed, given custom cover art, populated with new tracks, or pruned.
  - ☑️ **Multi-Select & Selective Delete**: Dedicated "Select" toggle button, top banner with selection count and "Select All" / "Deselect All", per-track checkboxes, and bottom floating bar with confirmation dialog to batch delete selected tracks in one tap.
  - ✕ **Single-Track Instant Removal**: Clean remove button on each track for rapid 1-click library maintenance.
  - **Transparent High-Fidelity Audio**: Explicitly prioritizes YouTube WebM Opus audio streams (itag 251, ~160kbps, 48kHz sampling) over standard AAC, preserving full acoustic bandwidth up to 20kHz with crystalline treble, deep bass response, and zero harsh compression artifacts.
  - **Smart Bitrate Negotiation**: Seamlessly maps Low, Medium, and Max/High quality settings with Opus and AAC fallbacks for optimal bandwidth efficiency.
- 🌊 **32-Bit Floating Point Audio Sink (v3.1)**:
  - **Studio Headroom & Dynamic Range**: ExoPlayer decodes and processes audio through a 32-bit floating point PCM audio sink (`setEnableFloatOutput(true)`), preventing digital clipping and truncation distortion during volume scaling and EQ processing.
- 🎚️ **EBU R128 DynamicsProcessing Peak Limiter (v3.1)**:
  - **Studio Loudness Normalization**: Integrated Android hardware `DynamicsProcessing` limiter on API 28+ configured with a -1.0 dBFS true-peak threshold and studio target gain towards -14 LUFS, eliminating abrupt loudness jumps between acoustic tracks and loud masters.
- 🎯 **Official Topic Stream Prioritization (v3.1)**:
  - **YouTube Music Filtering**: Search results and playlist imports prioritize official artist channels (`- Topic`, `VEVO`, `Official Audio`) while strictly discarding amateur re-uploads and bootlegs.
- 🧠 **Pure Kotlin On-Device ML Vector Engine (v3.1)**:
  - **Zero-Overhead 32D Embeddings**: On-device vector engine calculating cosine similarities and iALS folding-in user centroids in microseconds without native C++ overhead.
  - **Negative Hyperplane Carving**: Disliked songs carve out a negative subspace to immediately suppress unwanted genres, moods, or styles from Made For You.
  - **Contextual Multi-Armed Bandits (LinUCB)**: Introduces exploration bonuses to discover promising new artists from the affinity graph without disrupting playlist flow.

- 🚀 **In-App OTA Auto-Updater (v3.0)**:
  - **Automated Update Discovery**: Checks GitHub releases automatically in the background using lightweight OkHttp client.
  - **In-App Download & Install**: Interactive dialog displays version changelog, real-time download progress bar, and launches native Android package installer safely via secure `FileProvider`.
  - **Manual Trigger in Settings**: On-demand "Check for Updates" button in Settings screen with instant update status or version confirmation toast.
- 🎯 **Made For You Feedback & Negative Queue Purge (v3.0)**:
  - **Direct Like / Dislike Controls**: Integrated dynamic thumbs up / thumbs down controls right inside Player Bottom Sheet for Made For You tracks.
  - **Auto-Skip & Queue Purge**: Giving negative feedback (thumbs down) instantly records a negative affinity score, auto-skips immediately to the next song, and purges all copies/variants of the disliked track from the active playback queue.
- 🧼 **Canonical Variant Song Deduplication (v3.0)**:
  - **Acoustic & Title Normalization**: Strips YouTube upload metadata artifacts (`(Official Video)`, `[Lyrics]`, `(Audio)`, `4K`, `Remastered`, etc.) and primary artists.
  - **Levenshtein Fuzzy Deduplication**: Eliminates redundant recommendations across Made For You, curated mixes, and discovery lists.

- 🛡️ **100% Rock-Solid Playback Stability (v2.9)**: Permanently eliminated the exact crash causing the app to close after ~6–8 seconds into playback.
  - **Cross-Thread ExoPlayer Violation Eliminated**: Pinpointed via live ADB device logcat that background stream prefetching (`prefetchJob` after 8s) and track pre-caching were reading `player.playbackState` from `Dispatchers.IO` (`DefaultDispatcher-worker`), violating Media3 ExoPlayer's strict single-thread rule (`IllegalStateException: Player is accessed on the wrong thread`).
  - **Thread-Safe Atomic Buffering Shield**: Added `@Volatile var isBuffering` to `MusicPlayer` synchronized directly with `Player.Listener` events on the Main thread. Background coroutines now monitor buffering safely without ever querying `ExoPlayer` across threads.
  - **Universal Main-Thread Dispatch Guarantees**: Enforced main-thread execution on all playback controls (`playSong`, `togglePlayPause`, `playNext`, `playPrevious`) to prevent any background-thread player invocations.
- ⚡ **Instant Playback & Zero-Deadlock Streaming Engine**: Resolved the playback stall and idle deadlock issue. Corrected ExoPlayer's `DefaultHttpDataSource` redirect handling on YouTube CDN streams, eliminated `STATE_IDLE` playback deadlocks on song selection, tuned initial playback buffering to 1,500ms for instantaneous first-tap start, safely recycle OkHttp socket connections, and prioritize hardware-accelerated M4A/AAC streams.
- 📶 **Poor & Fluctuating Network Resilient Streaming**: Completely overhauled playback error handling and stream extraction to eliminate rapid, erratic song skipping on poor or fluctuating connections. ExoPlayer now withstands transient packet loss, signal dips, and handoffs with a fast 3-attempt exponential backoff retry policy (`DefaultLoadErrorHandlingPolicy(3)`).
- 🔄 **Non-Skipping Self-Healing Stream Recovery**: Network timeouts, socket drops, and expired CDN URLs will NEVER skip through the playlist. The player automatically retries with exponential backoff and transparently resumes at the exact interrupted millisecond via native `setMediaItem(mediaItem, startPositionMs)` with zero double-buffering.
- 🎚️ **Adaptive Low-Bitrate Fallback & LRU Stream Caching**: Integrated an in-memory `LruCache` for stream URLs and added automatic fallback to lightweight ~48–70 kbps Opus/AAC streams when higher bitrates encounter network congestion, saving up to 70% bandwidth and playing smoothly on 2G/3G/poor 4G.
- 🛡️ **Bandwidth-Aware Safe Prefetching**: Prefetching now gives 100% network priority to active playback. Background caching waits until the active song is comfortably buffered, aborts if the player is actively buffering, and avoids heavy audio byte downloads on metered connections.
- ⚡ **Expanded Buffer Cushions & Stutter Elimination**: Increased HTTP connect/read timeouts to 25s, optimized initial buffer to 1,500ms, and rebuffer recovery cushion to 2,500ms, permanently eliminating 1-second start-stop stutter loops on high network jitter.
- 🔁 **Instant Idle Playback Retry**: Tapping Play/Pause when the player is idle or recovering from network loss seamlessly re-initiates stream extraction and resumes the selected song immediately.

- 🎵 **Headless Service Playback Engine**: Completely migrated ExoPlayer media preparation, queue management, and `STATE_ENDED` track transitions from UI components into the headless background service (`MusicPlayer` / `PlaybackService`). Songs smoothly and autonomously transition to the next track with the phone screen off, locked, or backgrounded.
- 🛡️ **Zero-Pause State Synchronization**: Eliminated asynchronous `stop()` race conditions that previously flipped `isPlaying` to paused during track loading; crossfade volume initialization hardened against silent playback.
- 🌐 **Self-Healing Background CDN Recovery**: Error recovery for expired YouTube CDN tokens and HTTP 403 status codes operates autonomously at the service layer without needing the UI open.
- 🎛️ **Streamlined Settings Audio Quality (Low, Medium, Max)**: Clean, modern segmented buttons (`Low`, `Medium`, `Max`) mapped directly to optimal Opus and AAC stream profiles.
- 🧹 **Clean Library UI**: Consolidated playlist creation inside the dedicated Playlists section.
- 🔒 **Permanent App-Close Playback Termination**: Swiping ATune away from Recents or exiting immediately and directly halts playback and clears notifications.

- 🚀 **Turbocharged Composition & Stable Key Diffing**: Added unique, stable keys across all LazyLists in every screen, eliminating unnecessary recompositions and redundant image fetches during scrolling.
- 🔋 **Lifecycle-Aware Flow Collection**: Upgraded 30+ root and screen flow collectors to `collectAsStateWithLifecycle()`, cutting CPU usage and preserving battery when the app is backgrounded.
- 🧠 **Global Coil Singleton Image Cache**: Integrated `ImageLoaderFactory` with 15% RAM cache and 100MB disk cache, reusing cached bitmaps everywhere and saving cellular bandwidth.
- ⚡ **Optimized ExoPlayer Buffer & 60% Memory Cut**: Refined buffer boundaries (20s/60s) for responsive playback starts and zero network waste on track skips.
- ⚡ **Instant-Load Staggered Network Streaming**: Primary Trending songs render immediately on startup (~300ms) with zero spinner delay, while regional playlists stream in progressively.
- 📂 **Direct Playlist URL Import in Library**: Exposed direct playlist URL importing right from the Saved Playlists header.
- 🗄️ **Room Indexing & SQLite Write-Ahead Logging (WAL)**: Indexed playback timestamps and play counts, with WAL enabling concurrent reads while writes persist seamlessly.
- 🎯 **Multi-Dimensional "Made For You" Preference Engine**: Explicit multi-dimensional feedback across 7 dimensions (Language, Industry, Mood, Production Style, Theme, Singer/Artist, and Vocal Timbre). Thumbs-up immediately queries and expands similar tracks, while thumbs-down permanently filters out unwanted vibes.
- 🎛️ **Interactive Taste Preferences & Feedback Manager**: Handpick, review, and undo your "Loved & Boosted" and "Tuned Out / Hidden" feedbacks anytime via the dedicated Taste Preferences manager in the Made For You section.
- 🎧 **Zero-Interruption Voice Assistant Interaction**: Smart headphone detection keeps music playing at **100% full volume with ZERO ducking** when earbuds or headphones are connected, while providing subtle background ducking on loudspeakers.
- 📻 **AI Radio DJ Commentary**: Real-time charismatic radio host commentary introducing and hyping up songs and transitions, customized to your Taste DNA archetype.
- 📖 **"Explain This Song" Deep Dive**: In-depth breakdowns of song storylines, cultural metaphors, lyrical wordplay, and sonic arrangement.
- ⚡ **Multi-Threaded Turbo Downloads (MB/s Speeds)**: Converted single sequential streams into 4 concurrent HTTP Range segmented downloads using `RandomAccessFile` chunk streaming, bypassing CDN rate limits for ultra-fast multi-megabyte per second downloads.
- 🎤 **Robust Multi-Tier Lyrics Engine**: Exact-match Tier 0 LRCLIB (`/api/get`), safe null-resilient JSON parsing, multi-pass search fallback, and `lyrics.ovh` integration for instant, rock-solid synchronized karaoke lyrics.
- 🎚️ **Audiophile Punch & 3D Spatial Audio**: DynamicsProcessing limiter unclamped for physical low-end power, +12 dB sub-bass shelf with 230 Hz warmth, forced Transaural 3D virtualization for phone speakers & headphones, and self-healing session recovery.
- 🛡️ **Smooth Uninterrupted Playback**: Disabled aggressive silence-skipping and eliminated accidental tap-to-seek triggers during lyrics scrolling, ensuring songs never fast-forward or jump ahead unexpectedly.
- 🎨 **Official 3D Adaptive Branding & Material You Theming**: Modern 3D ribbon monogram and electric cyan soundwave with layered adaptive icons, sub-pixel alpha matting, and dynamic Android 13+ wallpaper theming.
- 📥 **Persistent WorkManager Background Downloads**: Crash- and reboot-resilient background download pipeline with live speed monitoring (KB/s, MB/s), pause/resume flags, and unmetered (WiFi-only) network constraint controls.
- 🔄 **Auto-Healing 403 Stream URL Refresh**: Seamlessly recovers from expired YouTube stream tokens and HTTP 403 errors, resuming playback at the exact second without skipping.
- ⚡ **Zero-Latency Next-Track Pre-Caching**: Automatically pre-buffers 2 MB of upcoming songs at 80% playback progress for seamless, instant transitions.
- 📱 **Interactive Material You Home Screen Widget**: 4x2 interactive home screen widget with dynamic accent theming, playback controls, album art, and like toggle.
- 🚗 **Android Auto & MediaBrowser Integration**: Upgraded `PlaybackService` to `MediaLibraryService` for seamless browsing and playback on Android Auto dashboards and wearable head units.
- 🎧 **Instant Music Streaming & Search**: Search millions of tracks online with instant streaming powered by Media3 ExoPlayer.
- 🔐 **Hardware-Backed AES-256 GCM Key Security**: AI Studio credentials and API keys are encrypted at rest using Android KeyStore hardware security.
- 📦 **R8 Ultra-Compact Release Packaging**: Footprint reduced down to **~4.70 MB** with resource shrinking and custom ProGuard keep rules for Media3, Room, NewPipeExtractor, and Coil.
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
   - Alternatively, download [**ATune-v3.0.apk**](https://github.com/TusharTyagi-63/ATune-App/releases/download/v3.0/ATune-v3.0.apk).
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
| **Version** | 3.0 |
| **APK File** | ATune-v3.0.apk / ATune-latest.apk |
| **File Size** | ~4.74 MB |
| **Minimum OS** | Android 8.0 (API level 26) or higher |
| **Architecture** | Universal (ARM64, ARMv7, x86_64) |

---

<p align="center">Made with ❤️ by <a href="https://github.com/TusharTyagi-63">TusharTyagi-63</a></p>
