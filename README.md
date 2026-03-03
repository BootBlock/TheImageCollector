# The Image Collector

A privacy-focused media browser and downloader for Android and Windows.

Browse content from Reddit, RedGifs, Google Images, and Imgur in one place. Save what you like to a local library with tagging, ratings, and search. On Android, store media in an encrypted vault that locks behind a password or biometrics.

## ✨ Features

### 🌐 Multi-Source Browsing

- **Reddit** - subreddits, user pages, home feed, saved posts. All sort modes (hot/new/top/rising). Signed-in feeds on Android via cookie auth.
- **RedGifs** - trending, top-this-week, search, and explore feeds.
- **Google Images** - keyword search with safe-search toggle.
- **Imgur** - search with pagination.

Sources are scraping-based (Reddit, Google, Imgur) or API-based (RedGifs). Scraping sources can break if the upstream site changes layout.

### 🖼️ Viewer

Full-screen viewer with swipe navigation between posts, pinch-to-zoom, and video playback with autoplay/mute/loop controls. Multi-image gallery posts expand into a nested viewer.

Other viewer features:
- Slideshow mode with configurable interval
- Swipe-to-dismiss
- Ambilight effect (blurred ambient glow behind media)
- Brightness boost (Android)
- Metadata HUD overlay
- Image cropping before save
- Share, open permalink, set as wallpaper, cast to Chromecast, or present to a secondary monitor
- Media preloading for neighbouring posts (configurable, off by default)

### ⬇️ Downloads

- Configurable concurrent download limit (1-8) and per-host delay
- Max download size cap
- Default collection assignment
- Save post metadata (title, author, comments) alongside media
- Failed-downloads log with retry
- Custom storage path on desktop with migration support

### 🔄 Auto-Download

Define saved feeds (subreddit, user, home, saved, Google Images, Imgur search) that run on a schedule:
- 6/12/24-hour intervals
- Android: background execution via WorkManager (Wi-Fi only) with foreground service
- Desktop: runs while the app is open
- Duplicate detection across runs (tracks up to 5,000 seen URIs)
- Run-on-demand button

### 📚 Library

Local SQLite database for all downloaded media.

**Organisation:**
- Collections, user labels (named + coloured), colour labels, free-form tags, notes, numeric rating, favourite and NSFW toggles

**Search & Filter:**
- Full-text search (FTS5, prefix matching)
- Filter by favourites, colour label, NSFW, media type (image/video/gif), user label
- Saveable filter presets with icon and colour

**Sort:** date, title, size, rating

**Other:**
- SHA-256 and perceptual hash (pHash) duplicate detection
- File import via drag-and-drop or file picker (deduplicates by hash)
- Aggregate library statistics

### 🔒 Vault (Android)

Encrypted media storage with a separate encrypted database.

- Password or PIN protection (minimum 6 characters)
- AES encryption with PBKDF2-derived key
- Optional biometric unlock (Android Keystore)
- Auto-lock on configurable timeout (1/5/15/60 minutes)
- Route new downloads directly into the vault
- Optional secure erase (zero-overwrite before delete)
- Full vault wipe
- Decrypted temp files cleaned up on lock and startup
- If you forget the vault password, the only recovery is wiping vault data

### 📦 Subreddit Packs

Curated bundles of subreddits distributed as `.ticr` files (ZIP with a JSON manifest, optionally AES-256 encrypted). Packs sync from this repository via the GitHub Contents API. Install, update, or remove packs from the UI. Each pack includes subreddit metadata: display name, description, NSFW flag, tags, and default sort/time range.

### 🛡️ Privacy

- **App Lock** - biometric or device PIN/pattern gate on launch
- **Decoy Screen** - a working calculator that hides the real app; long-press the display to return
- **Screenshot Protection** - prevents screenshots and screen recording on Android (`FLAG_SECURE`)
- **Immersive Mode** - hides Android status and navigation bars
- **No telemetry**

### 📺 Casting & Presentation

- **Chromecast** - device discovery, connect/disconnect, cast images and videos (opt-in)
- **Presentation Mode** (desktop) - spawn a frameless full-screen projector window on a secondary display, with video seek/play/pause bridged via IPC
- **Pop-out Viewer Window** (desktop) - standalone window for individual media items

### 🎨 Wallpaper

Set any library image as the desktop wallpaper (Windows and Linux).

### 💾 Backup & Restore

Export app data as a `.ticbackup` file (ZIP):
- Optional passphrase encryption (AES)
- Include or exclude vault data
- Inspect backup contents before restoring
- Selective restore (library, vault, or both)
- Android: share via system sheet or save to Downloads
- Desktop: native file picker

### ⬆️ Updates

Checks GitHub Releases for new versions with semver comparison. Shows current vs. latest version and links to the releases page.

### 🔍 Reverse Image Search

Look up source context for any image - checks the local library first, then offers external search via SauceNAO, TinEye, or Google Lens.

## 📱 Platforms

| Platform | Status |
|---|---|
| Android | Primary target. Full feature set. |
| Windows | Supported. Presentation mode, pop-out windows, wallpaper, drag-and-drop import. |
| Web | Debug build target only. |

## 📥 Install

### Android

1. Download `app-release.apk` from [GitHub Releases](../../releases).
2. Allow installation from unknown sources when prompted.
3. Open the APK to install.

### Windows

1. Download the Windows build from [GitHub Releases](../../releases).
2. Extract the archive.
3. Run the executable.

## 🛠️ Tech Stack

- **Flutter & Dart** (SDK 3.11+)
- **Riverpod** for state management
- **Drift** (SQLite) for local databases with FTS5 search
- **Dio** for HTTP
- **GoRouter** for navigation
- Material 3 with Dynamic Color theming

## 📝 Notes

- Scraping-based sources can break if the upstream site changes.
- Some content may require signing in via the site itself; behaviour varies by source.

## ⚖️ Licence

All rights reserved.
