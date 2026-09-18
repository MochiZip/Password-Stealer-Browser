# 🛰️ Mochi Vault — Browser Data Manager & Web Dashboard
> **Made By MochiMochHT3 On Github**

A single-file toolset that extracts browser data, decrypts profiles, and compiles everything into a stunning interactive local web dashboard. Ships as a double-clickable **macOS app** that unlocks itself automatically.

---

## 🍎 It's an App Now

Double-click **`MochiVault.app`** — it extracts everything, unlocks your encrypted credentials by itself, and opens your dashboard. No terminal required.

Rebuild the app bundle anytime (e.g. after edits) with:

```bash
./make_app.sh
```

**First-time setup (one minute):**
1. **Grant Full Disk Access:** `System Settings → Privacy & Security → Full Disk Access` → add **MochiVault.app**.
2. Double-click the app. It asks for your **macOS login password once** so it can unlock the keychain and decrypt your credentials.
3. Done. The password lives only in the **system Keychain** (encrypted) and is used automatically on every launch from then on.

> The app never stores your password in a file. Read it back or remove it anytime with `security find-generic-password -s MochiVault -a macos-login-password -w` / `dashboard.py forget`.

---

## 📌 Quick Start (terminal)

```bash
cd /Users/elimochi/Downloads/browser
./launch_dashboard.sh
```

This runs the extraction binary, compiles the dashboard, and opens it in your browser. If a vault password is stored in the Keychain, decryption happens automatically — no prompts.

---

## 🧰 One File, Every Command

Everything lives in **`dashboard.py`**. No more juggling multiple scripts.

| Command | What it does |
| --- | --- |
| `python3 dashboard.py build` | Compile `~/results/dashboard.html` from the extracted JSON, then open it |
| `python3 dashboard.py build --no-open` | Compile only, without opening the browser |
| `python3 dashboard.py clear "keyword"` | Remove matching history entries from `history.json`, then auto-rebuild the dashboard |
| `python3 dashboard.py show` | Print everything recovered, right in the terminal |
| `python3 dashboard.py show history` | Print a single category (password / history / bookmark / cookie / download / extension / localstorage / sessionstorage) |
| `python3 dashboard.py setup` | Store the macOS login password in the Keychain once → decryption is automatic forever |
| `python3 dashboard.py forget` | Remove the stored keychain password |
| `python3 dashboard.py merge src dst` | Utility — append one file to the end of another |

### Example

```bash
python3 dashboard.py setup          # one time, then never asked again
python3 dashboard.py clear "YouTube"
python3 dashboard.py show cookies
python3 dashboard.py build
```

---

## 🌐 About the Dashboard

The generated page is a full glassmorphism command center:

- **Animated ambient background** with drifting gradient orbs
- Safari ⇄ Brave segmented switcher with a sliding gradient indicator
- Six data panes per browser: **Passwords · History · Bookmarks · Cookies · Downloads · Extensions**
- Live-updating hero stats with count-up animations and a real-time clock
- Instant fuzzy search with live result counts
- One-click **Copy** for credentials/cookies with toast feedback
- Per-row **Delete** on history (confirm → copies a ready-to-run purge command)
- Human-readable timestamps ("Tue Sep 17 · 11:05 AM · 2h ago")
- Fully responsive — collapses to a clean stacked layout on mobile

---

## 🔒 Prerequisites

1. **Full Disk Access:** `System Settings → Privacy & Security → Full Disk Access` → enable your **Terminal**.
2. **Close running browsers** (`Cmd + Q`) before extraction to avoid database lock errors.
3. Grant execution permission once: `chmod +x cats dashboard.py launch_dashboard.sh`.

---

## 🗃️ What Gets Recovered

| File | Contents |
| --- | --- |
| `password.json` | Saved credentials |
| `history.json` | Browsing history |
| `bookmark.json` | Bookmarks |
| `cookie.json` | Cookies |
| `download.json` | Download records |
| `extension.json` | Installed extensions |
| `localstorage.json` / `sessionstorage.json` | Web storage data (terminal view only) |