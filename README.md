# The Image Collector

A privacy-focused media browser and downloader for Android and Windows.

Browse content from Reddit, RedGifs, Google Images, and Imgur in one place. Save what you like to a local library with tagging, ratings, and search. On Android, store media in an encrypted vault that locks behind a password or biometrics.

---

## 🚀 Quick Start

### Install

**Android:**

1. Download `app-release.apk` from [GitHub Releases](../../releases).
2. Allow installation from unknown sources when prompted.
3. Open the APK to install.

**Windows:**

1. Download the Windows ZIP (x64 or ARM64) from [GitHub Releases](../../releases).
2. Extract the archive to a folder of your choice.
3. Run `the_image_collector.exe`.

### First Run

1. **Choose a startup destination** — Sources, Library, or Downloads. You can change this later in Settings.
2. **Browse a source** — tap Sources and pick Reddit, RedGifs, Google Images, or Imgur. Enter a subreddit name, search term, or explore the available feeds.
3. **View media** — tap any thumbnail to open the full-screen viewer. Swipe left/right to navigate between posts. Pinch to zoom images, and tap videos to play.
4. **Download** — tap the download button in the viewer or long-press a thumbnail. Media is saved to your local library.
5. **Organise** — open the Library tab to tag, rate, label, and search your saved media.

### Optional Setup

- **Reddit sign-in** (Android) — go to Sources → Reddit → Home or Saved tab and sign in via the Reddit login page. This unlocks your home feed, saved posts, and subscriptions. Your cookies are stored in secure storage and never leave the device.
- **NSFW content** — enable the NSFW toggle in Settings to access age-restricted subreddits. Your Reddit account must also have age verification enabled on reddit.com.
- **Vault** (Android) — go to Settings → Vault to set a password and enable encrypted media storage.
- **Subreddit packs** — go to Sources → Reddit → Packs to browse and install curated bundles of subreddits.

---

## ✨ Features

### 🌐 Multi-Source Browsing

- **Reddit** — subreddits, user pages, home feed, saved posts. All sort modes (hot, new, top, rising). Signed-in feeds on Android via cookie auth.
- **RedGifs** — trending, top-this-week, search, and explore feeds.
- **Google Images** — keyword search with safe-search toggle.
- **Imgur** — search with pagination.

Sources are scraping-based (Reddit, Google, Imgur) or API-based (RedGifs). Scraping sources can break if the upstream site changes layout — see [Troubleshooting](#-troubleshooting) below.

### 🖼️ Viewer

Full-screen viewer with swipe navigation between posts, pinch-to-zoom, and video playback with autoplay/mute/loop controls. Multi-image gallery posts expand into a nested viewer.

- Slideshow mode with configurable interval
- Swipe-to-dismiss
- Ambilight effect (blurred ambient glow behind media)
- Brightness boost (Android)
- Metadata HUD overlay
- Image cropping before save
- Share, open permalink, set as wallpaper, cast to Chromecast, or present to a secondary monitor
- Media preloading for neighbouring posts (configurable, off by default)

### ⬇️ Downloads

- Configurable concurrent download limit (1–8) and per-host delay
- Max download size cap
- Default collection assignment
- Save post metadata (title, author, comments) alongside media
- Failed-downloads log with retry
- Custom storage path on desktop with migration support

### 🔄 Auto-Download

Define saved feeds (subreddit, user page, home, saved, Google Images, Imgur search) that run on a schedule:

- 6/12/24-hour intervals
- Android: background execution via WorkManager (Wi-Fi only) with foreground service notification
- Desktop: runs while the app is open
- Duplicate detection across runs (tracks up to 5,000 seen URIs per feed)
- Run-on-demand button for each saved feed

### 📚 Library

Local database for all downloaded media.

**Organisation:**
- Collections, user labels (named + coloured), colour labels, free-form tags, notes, numeric rating, favourite and NSFW toggles

**Search & Filter:**
- Full-text search with prefix matching
- Filter by favourites, colour label, NSFW, media type (image/video/gif), user label
- Saveable filter presets with icon and colour

**Sort:** date, title, size, rating

**Other:**
- Duplicate detection by file hash (SHA-256) and visual similarity (perceptual hash)
- File import via drag-and-drop or file picker (deduplicates automatically)
- Aggregate library statistics

### 🔒 Vault (Android)

Encrypted media storage with a separate encrypted database.

- Password or PIN protection (minimum 6 characters)
- AES-256 encryption with PBKDF2-derived key (600,000 iterations)
- Optional biometric unlock (fingerprint or face via Android Keystore)
- Auto-lock on configurable timeout (1/5/15/60 minutes)
- Route new downloads directly into the vault
- Optional secure erase (zero-overwrite before delete)
- Full vault wipe
- Decrypted temp files cleaned up on lock and startup
- **If you forget the vault password, the only recovery is wiping vault data**

### 📦 Subreddit Packs

Curated bundles of subreddits distributed as `.ticr` files. Packs are synchronised from this repository and can be installed, updated, or removed from the app. Each pack includes subreddit metadata: display name, description, NSFW flag, tags, and default sort/time range. Packs can optionally be AES-256 encrypted.

### 🛡️ Privacy

- **App Lock** — biometric or device PIN/pattern gate on launch
- **Decoy Screen** — a fully working calculator that hides the real app; long-press the calculator display to return
- **Screenshot Protection** — prevents screenshots and screen recording on Android
- **Immersive Mode** — hides Android status and navigation bars
- **No telemetry** — zero data collection, no analytics, no tracking

### 📺 Casting & Presentation

- **Chromecast** — device discovery, connect/disconnect, cast images and videos (opt-in via Viewer settings)
- **Presentation Mode** (desktop) — full-screen projector window on a secondary display with synchronised video controls
- **Pop-out Viewer Window** (desktop) — standalone window for individual media items

### 🎨 Wallpaper

Set any library image as the desktop wallpaper (Windows and Linux).

### 💾 Backup & Restore

Export app data as a `.ticbackup` file:

- Optional passphrase encryption (AES)
- Include or exclude vault data
- Inspect backup contents before restoring
- Selective restore (library, vault, or both)
- Android: share via system sheet or save to Downloads
- Desktop: native file picker

### ⬆️ Updates

The app checks GitHub Releases for new versions. Shows current vs. latest version and links directly to the releases page.

### 🔍 Reverse Image Search

Look up source context for any image — checks the local library first, then offers external search via SauceNAO, TinEye, or Google Lens.

---

## 📱 Platforms

| Platform | Status |
|---|---|
| Android | Primary target. Full feature set including vault, app lock, decoy screen, background auto-download, biometric unlock, screenshot protection, and brightness boost. |
| Windows | Supported. Includes presentation mode, pop-out viewer windows, wallpaper setting, drag-and-drop import, and custom storage path. |

---

## ❓ Troubleshooting

### NSFW subreddits are blocked or show an age-verification page

**Symptoms:** Reddit NSFW subreddits return an error, a blank page, or an age-verification interstitial instead of content.

**Cause:** ISPs in the UK and some EU countries block access to NSFW subreddits at the network level to comply with age-verification regulations (e.g. the UK Online Safety Act / Ofcom requirements). This affects all scraping-based access from those networks.

**Solutions (try in order):**

1. **Sign in to Reddit** — go to Sources → Reddit → Home or Saved tab and sign in. Your Reddit account must have age verification enabled at [reddit.com/settings/account](https://www.reddit.com/settings/account). Signed-in access often bypasses the interstitial.
2. **Enable NSFW in app settings** — open Settings and enable the NSFW toggle. Without this, the app skips age-restricted content entirely.
3. **Use a VPN** — if your ISP blocks NSFW subreddits at the network level, a VPN routes your traffic through an unrestricted network and restores normal access. Any reputable VPN service will work.
4. **Switch network** — a mobile data connection or a different Wi-Fi network may not have the same ISP-level blocks.

### A source stopped working or returns no results

**Cause:** Reddit, Google Images, and Imgur are accessed via web scraping. If the upstream site changes its HTML layout, scraping can break until the app is updated.

**What to do:**

- Check [GitHub Releases](../../releases) for a newer version of the app.
- Google Images may also show a consent page or CAPTCHA on some networks. Try changing your User-Agent in Settings, switching networks, or waiting and trying again later.
- Imgur scraping can similarly be blocked. Retry later or on a different network.

### RedGifs feeds load slowly or stop loading

**Cause:** RedGifs has API rate limits. The app fetches multiple pages per load (configurable in Settings under "RedGifs pages per fetch", default 2). Higher values increase request volume and rate-limit risk.

**What to do:**

- Lower the "RedGifs pages per fetch" setting to 1.
- Wait a few minutes and try again — rate limits are typically short-lived.

### Reddit rate limiting (HTTP 429 errors)

**Cause:** Reddit throttles requests when too many are made in a short time.

**What to do:**

- Increase the "Reddit request spacing" in Settings (default 3,000 ms). Higher values reduce request frequency.
- Disable "Media preload" in Viewer settings if enabled — preloading neighbouring posts increases request volume.
- Avoid rapid swiping in the viewer, which triggers a request per post.

### Google Images shows a CAPTCHA or consent page

**Cause:** Google detects automated access and shows a challenge.

**What to do:**

- Open the link in your browser using "Open in browser" to complete the consent/CAPTCHA manually.
- Change the User-Agent string in Settings to mimic a different browser.
- Try again later or from a different network.

### Downloads fail or are incomplete

**What to check:**

- Ensure you have sufficient storage space.
- Check the failed-downloads log (Downloads tab → Failed) and retry individual items.
- If downloads for a specific host consistently fail, try increasing the per-host delay in Settings.
- On desktop, verify the custom storage path is writable.

### Vault password forgotten

**There is no recovery mechanism.** The vault uses AES-256 encryption with a key derived from your password. If you forget the password, the only option is to wipe vault data entirely from Settings → Vault → Wipe.

### App crashes or behaves unexpectedly

- Check for updates via Settings → About → Check for Updates.
- Try clearing the image cache in Settings.
- As a last resort, clear app data (Android: Settings → Apps → The Image Collector → Clear Data) or delete the app's data folder (Windows). This will erase your library and settings.

### Auto-download not running (Android)

- Ensure the saved feed schedule is set (6/12/24 hours).
- Check that battery optimisation is disabled for The Image Collector in Android Settings → Battery → Unrestricted.
- Auto-download requires a Wi-Fi connection by default. Switch to Wi-Fi or disable the Wi-Fi-only requirement if appropriate.
- The Android system may defer background work under Doze mode or if the device hasn't been charged recently.

---

## ⚖️ Licence

All rights reserved.
