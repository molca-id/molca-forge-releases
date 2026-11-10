# MolcaForge User Guide

A step-by-step guide to MolcaForge **0.2.0**. It covers everything that is new in this version and the everyday tasks you will do most.

**Contents**
1. [What's new in 0.2.0](#1-whats-new-in-020)
2. [Install](#2-install)
3. [Sign in and choose a module](#3-sign-in-and-choose-a-module)
4. [Connect your GitHub / GitLab / Bitbucket account](#4-connect-your-github--gitlab--bitbucket-account)
5. [Open, clone or create a project](#5-open-clone-or-create-a-project)
6. [Commit your work (the Changes list)](#6-commit-your-work-the-changes-list)
7. [Switch repositories and branches](#7-switch-repositories-and-branches)
8. [Beginner mode and the ? hints](#8-beginner-mode-and-the--hints)
9. [MolcaVault (preview)](#9-molcavault-preview)
10. [macOS notes](#10-macos-notes)
11. [Keyboard shortcuts](#11-keyboard-shortcuts)
12. [Troubleshooting](#12-troubleshooting)
13. [For maintainers: building and releasing](#13-for-maintainers-building-and-releasing)

---

## 1. What's new in 0.2.0

| Area | What changed |
| --- | --- |
| **Modules** | After sign-in you choose **MolcaRepo** (Git) or **MolcaVault** (office NAS, preview). The window title and icon follow the module you are in. |
| **Changes list** | One list instead of "Unstaged / Staged". **Tick a file to include it in the next commit.** No Stage / Unstage buttons any more; the checkbox does it. |
| **Selecting files** | **Shift+click** selects a range of files, **Ctrl+click** adds one. Then **Include**, **Exclude** or **Discard** them together. |
| **Accounts** | **Sign in with GitHub / GitLab / Bitbucket in your browser**, no token to copy. Each repository now picks the right account automatically. |
| **Folder fields** | A **Browse…** button next to every folder field, so you never have to copy and paste a path. |
| **Start screen** | Fits your window with no page scrollbar; two equal-height panels; search your local repositories; the Git guide opens as a popup. |
| **Beginner mode** | Small **?** icons on the key buttons explain them when you hover. The switch is also on the MolcaVault toolbar. |
| **Readability** | Hard-to-read text in the light and dark themes was fixed; dialogs use one consistent colour. |
| **Installer** | New artwork that matches the sign-in page, and a step-by-step log while installing. |
| **macOS** | A version for Apple Silicon and Intel Macs. |
| **Releases** | Pushing a version tag now builds both installers and publishes a GitHub Release automatically. |

---

## 2. Install

### Windows 10/11
1. Download `MolcaForge-Setup-<version>.exe` from the [Releases page](https://github.com/molca-id/molca-forge-releases/releases).
2. Run it. If Windows SmartScreen warns you (the installer is not code-signed yet), click **More info → Run anyway**.
3. Follow the wizard: **Welcome → Changelog → Installation folder → Shortcuts → Installing → Finish**.
   - On the **Installing** page the list shows what the installer is doing: checking that the app is not running, removing a previous version (your repositories and settings are kept), extracting files, registering the app, applying your shortcut/startup choices, and checking that Git is installed.
   - On the **Shortcuts** page choose a Desktop shortcut, a Start Menu shortcut and whether to run at Windows startup.
4. Make sure **Git ≥ 2.28** is installed ([Git for Windows](https://git-scm.com/download/win)).

### macOS
1. Download the `.dmg` that matches your Mac: `…-mac-arm64.dmg` for Apple Silicon (M1/M2/M3/M4), `…-mac-x64.dmg` for Intel.
2. Open the `.dmg` and drag **MolcaForge** to **Applications**.
3. The first time, macOS says the developer cannot be verified (the app is not notarized yet). Right-click the app → **Open** → **Open**. Or run once in Terminal:
   ```bash
   xattr -cr /Applications/MolcaForge.app
   ```
4. Install Git if you do not have it: `brew install git git-lfs` (or the Xcode Command Line Tools).

> **Updating:** there is no auto-update yet. Download the new installer from the Releases page and run it; it upgrades the existing install in place and keeps your repositories, accounts and settings.

---

## 3. Sign in and choose a module

1. Open MolcaForge. Click **Sign in with OHARA**; your browser opens the OHARA (Molca SSO) page. Sign in there and return to the app.
2. The **main menu** shows two cards:
   - **MolcaRepo**: Git version control. It also shows the repository you opened last.
   - **MolcaVault**: the office NAS (**Preview** with sample data).
3. To come back to the main menu at any time, click the **grid icon** next to the brand name at the top of the sidebar (tooltip *Main menu*).

---

## 4. Connect your GitHub / GitLab / Bitbucket account

You can connect accounts from the start screen (right panel, **Repositories from your accounts**) or from **Accounts & Online Repos** in the sidebar.

### Option A: sign in with your browser (recommended)
1. Click **Connect account** and choose GitHub, GitLab or Bitbucket.
2. Choose **Sign in with GitHub** (or GitLab/Bitbucket).
3. Your browser opens. Sign in and click **Authorize**. Within a few seconds the account shows up as connected. There is no token to copy.

This uses **Git Credential Manager**, which comes with Git for Windows. On macOS install it once with `brew install --cask git-credential-manager`. If it is not available, MolcaForge tells you and you can use a token instead.

### Option B: a personal access token
1. **Connect account** → pick the provider → **Use a personal access token**.
2. The dialog has an **Open token page** button with the right permissions pre-selected. Create the token, copy it, paste it in the field and click **Connect**.
3. Gitea / Codeberg / Forgejo and self-hosted servers use this option (change the *Server address* if needed).

The token is stored encrypted by your operating system (Windows or the macOS Keychain) and is only used to talk to that provider.

### Option C: auto-detect
Click **Auto-detect** to reuse accounts that are already signed in to Git Credential Manager (for example after you pushed to GitHub before). Nothing is copied into MolcaForge.

### Which account does a repository use?
You usually do not need to choose. MolcaForge looks at **all your connected accounts** and picks the one that can reach the repository:
- the account whose username owns the repository, or
- the only account on that server, or
- if you have several accounts on the same server (for example a work account and a personal account) and the repository belongs to an organization, the one that actually has access (preferring the one that can push).

If more than one account qualifies, the Assistant asks you to choose, and you can change it any time in **Repository settings → Account for this repository**.

---

## 5. Open, clone or create a project

On the MolcaRepo start screen you have three cards:

| Card | What it does |
| --- | --- |
| **Open project** | Open a folder on your computer that already uses Git (or that you want to turn into a repository). |
| **Clone from the internet** | Download a project from GitHub, GitLab, Bitbucket… Paste the URL and pick where to save it. |
| **New project** | Start an empty repository (initial branch name, README, `.gitignore`, license). |

**Folder fields have a Browse… button.** Click it, pick the folder in the system dialog, and the path is filled in for you. You can still type a path if you prefer.

Below the cards:
- **On this computer** lists repositories MolcaForge found on your PC plus the ones you opened before, newest first. Use the **search box** to filter by name or folder, **Add folder** to scan another parent folder, and the refresh icon to scan again. The list scrolls inside the panel.
- **Repositories from your accounts** lists every repository you can reach online, with a search box, an *on this computer* badge and a one-click **Clone** button.
- The footer button **New to Git? Learn the basics in 2 minutes** opens a short guide in a popup (the four steps plus a searchable glossary).

The two panels always stay the same height and adapt when you resize the window, so the page itself never needs a scrollbar.

---

## 6. Commit your work (the Changes list)

Open **Changes** in the sidebar. This is the heart of daily work.

### The idea
Git lets you choose *which* changed files go into the next commit. In MolcaForge that choice is simply a **checkbox**:

| Checkbox | Meaning |
| --- | --- |
| ☑ ticked | This file **is in** the next commit |
| ☐ empty | This file is **not** in the next commit (it stays safe on your computer) |
| ▣ half-ticked | **Part** of the file is included (you picked some lines in the diff) |

> **Where did Stage / Unstage go?** That is exactly what the checkbox does. *Ticking* = stage, *un-ticking* = unstage. The old two lists ("Unstaged" and "Staged") are now one list called **Changes**; its header shows how many files are in the commit, for example `Changes (7 · 2 in commit)`.

### A normal commit
1. **Tick** the files you want (or tick the box in the list header to include everything shown).
2. Type a **Summary** (a short message). A longer **Description** is optional.
3. Click **Commit N files**. If you want to send it right away, use **+ Push**, or click **Push** in the toolbar later.

Good to know:
- If you tick nothing, the button says **Commit all (n files)** and commits every change.
- **Co-author** adds a `Co-authored-by` line; **Amend last commit** changes the previous commit.
- Click a row to see its diff on the right. Double-click a row to toggle its checkbox.

### Select many files at once
- Click a file, then **Shift+click** another file to select the whole **range** between them.
- **Ctrl+click** (**⌘+click** on macOS) adds or removes a single file.
- Selected rows are highlighted and a bar appears above the list: **N files selected** with the buttons
  - **Include (n)**: include the selected files in the commit,
  - **Exclude (n)**: leave them out (the files are kept),
  - **Discard (n)**: throw away their changes. Discarded changes are **always backed up to Stash**, and you get a confirmation first.
- **Shift+click on a checkbox** includes (or excludes) the whole range from the file you last clicked.

### Part of a file
Open a file's diff and use the buttons at the top of each hunk: **Include hunk**, **Exclude hunk**, **Discard hunk**. You can also click individual green/red lines first (Shift+click for a range) to include just those lines. A file with only some lines included shows a half-ticked checkbox.

### Filters
Use the search box and **Filter** button to narrow the list by status (New / Modified / Deleted / Renamed) and file extension. The header checkbox, **Discard all** and **Commit all** then apply only to the files shown.

### Beginner shortcuts
With Beginner mode on, a small bar above the list shows the four steps: **1. Edit → 2. Tick files → 3. Commit → 4. Push**, highlighting where you are.

---

## 7. Switch repositories and branches

- **Repository** (top of the sidebar): the dropdown lists **all repositories on your computer** (the same list as *On this computer*), newest first. Click one to switch. It scrolls if the list is long. To open, clone or create another project, choose **Close repository** in the avatar menu (top right) to return to the start screen, or search for it in the Command Palette (`Ctrl+K`).
- **Current branch** (below it): click to switch branches. Double-click a branch in the *Local branches* list to switch, right-click for more options. Uncommitted changes are saved to Stash automatically when needed.
- The arrows ↑ / ↓ on the branch show commits not pushed / not pulled yet.

---

## 8. Beginner mode and the ? hints

Beginner mode adds explanations around the app:
- a small **?** at the top-right corner of the key buttons. **Hover** the **?** to read what the button does. The **?** is next to the button, so it works even when the button is greyed out, and clicking it never runs the button.
- the four-step bar above the Changes list, and helper texts in the History and Branches pages.

Where the **?** appears:

| Module | Buttons with a ? |
| --- | --- |
| MolcaRepo toolbar | **Fetch**, **Pull**, **Push / Publish**, **Stash**, **Undo commit** |
| MolcaRepo sidebar | the **Repository** and **Current branch** pickers |
| MolcaRepo commit box | **Commit** and **+ Push** |
| MolcaVault toolbar | **Upload**, **New folder**, **Explorer / Finder** |

**Turn it on or off**, whichever is closest:
- the avatar menu at the top right → **Beginner mode**,
- the **Beginner mode** button on the MolcaVault toolbar (it shows a green dot when on),
- **Vault settings → Beginner mode**.

It is one setting shared by both modules.

---

## 9. MolcaVault (preview)

MolcaVault is the office NAS module. In this version it is a **preview with sample data**: you can click around and try the workflow, but it is not connected to the real NAS yet, and a banner says so. Use **Give feedback** to tell us what is confusing or missing.

What you can try:
- **Browse** the sidebar: **Home**, **My folder**, **All files**, **Recently changed**, **Favorites**, and the folder tree (**Proyek**, **Aset**, **Arsip**, …).
- **Upload**, **New folder** and **Explorer / Finder** on the toolbar (with ? hints in Beginner mode), plus the search box (`Ctrl+K`).
- **Transfers** shows uploads and downloads, including one that was interrupted and can be resumed.
- **Vault settings** shows the NAS connection and transfer behavior. The **Beginner mode** switch is here too.
- **Vault guide** is a short in-app guide with a glossary of NAS terms.

---

## 10. macOS notes

The macOS app is the same app with a few platform differences:
- **Window:** the native macOS title bar, with the window buttons on the left.
- **Shortcuts:** `⌘` replaces `Ctrl` (for example `⌘K` for the Command Palette, `⌘+click` to add a file to a selection). The keyboard-shortcuts dialog (`⌘/`) shows the Mac versions.
- **Files:** "File Explorer" becomes **Finder**; "Open in Terminal" opens Terminal.
- **Code editors** are detected from `/Applications` (VS Code, Cursor, VSCodium, Sublime Text, JetBrains IDEs).
- **Git:** the Homebrew `PATH` and your login-shell `PATH` are picked up automatically, even when you open the app from the Dock.
- **Tokens** are stored in the macOS Keychain.
- **First launch:** see [Install → macOS](#macos) for the "unverified developer" prompt.
- **MolcaVault:** the preview's sample data uses Windows-style SMB paths; real NAS integration on macOS is not set up yet.

---

## 11. Keyboard shortcuts

Press `Ctrl+/` (`⌘/` on macOS) in the app for the full list. The most useful ones:

| Action | Windows | macOS |
| --- | --- | --- |
| Command Palette (search any action) | `Ctrl+K` | `⌘K` |
| Go to Changes / History / Branches | `Ctrl+1` / `2` / `3` | `⌘1` / `2` / `3` |
| App settings | `Ctrl+,` | `⌘,` |
| Keyboard shortcuts | `Ctrl+/` | `⌘/` |
| Fetch / Pull / Push | `Ctrl+Shift+T` / `Ctrl+Shift+L` / `Ctrl+P` | `⌘⇧T` / `⌘⇧L` / `⌘P` |
| Commit (from the message box) | `Ctrl+Enter` | `⌘Enter` |
| Open in code editor | `Ctrl+Shift+A` | `⌘⇧A` |
| Zoom in / out / reset | `Ctrl +` / `Ctrl −` / `Ctrl 0` | `⌘ +` / `⌘ −` / `⌘ 0` |
| Select a range of files | `Shift+click` | `Shift+click` |
| Add one file to a selection | `Ctrl+click` | `⌘+click` |

---

## 12. Troubleshooting

**"Git was not found" / git commands fail**
Install Git ≥ 2.28 and reopen MolcaForge. Windows: [Git for Windows](https://git-scm.com/download/win). macOS: `brew install git git-lfs`.

**"detected dubious ownership in repository…"**
Git refuses a folder owned by a different Windows/macOS user. If you trust the folder, mark it as safe in a terminal, then reopen the repository:
```bash
git config --global --add safe.directory "<full path of the repository>"
```

**Sign in with GitHub/GitLab does nothing, or says Git Credential Manager is unavailable**
Git Credential Manager is required for browser sign-in. It ships with Git for Windows; on macOS run `brew install --cask git-credential-manager`. Or connect with a **personal access token** instead.

**The wrong account is used for a repository, or push is rejected for permissions**
Open **Repository settings → Account for this repository** (or click the **Choose account** button the Assistant shows) and pick the account that has access. If the remote uses SSH, the same page offers to switch it to HTTPS so the chosen account can be used.

**Windows SmartScreen / macOS "unverified developer" warning**
The installers are not signed or notarized yet. See [Install](#2-install) for how to open them. Distribution without these warnings needs a code-signing certificate (Windows) and an Apple Developer ID with notarization (macOS).

**I cannot see the ? icons**
Beginner mode is off. Turn it on from the avatar menu (see [Beginner mode](#8-beginner-mode-and-the--hints)).

**I discarded something by mistake**
Discarded changes are backed up to **Stash** first. Open **Stash** in the sidebar and apply the entry named *MolcaForge backup: discarded changes…*. **Time Machine** can also take you back to earlier points.

---

## 13. For maintainers: building and releasing

### Build locally
```bash
npm install
npm run dist          # Windows installer  → release/MolcaForge-Setup-<version>.exe
npm run dist:portable # Windows portable
npm run dist:mac      # macOS .dmg + .zip  → must run on a Mac
```
electron-builder cannot build macOS packages on Windows or Linux, which is why releases are built on GitHub Actions.

### Publish a release (automated)
1. Set `version` in `package.json` (for example `0.3.0`).
2. Update `build/changelog.txt` (shown in the Windows installer's *Changelog* page; keep it plain ASCII) and `build/release-notes.md` (the GitHub Release description). Both are in English.
3. Commit and push, then push a tag that is **exactly** the version:
   ```bash
   git tag v0.3.0
   git push origin v0.3.0
   ```
4. The **Build desktop apps** workflow (`.github/workflows/build.yml`) builds Windows and macOS (Apple Silicon + Intel). **Only if both succeed** it creates the GitHub Release with every installer attached. It also checks that the tag matches `package.json`, and fails otherwise.
5. If a build fails, fix it, then delete and re-push the tag (`git push origin :refs/tags/v0.3.0`, then tag again). No Release exists until all builds pass.

To try the builds without releasing, run the workflow manually (**Actions → Build desktop apps → Run workflow**); the installers appear as downloadable artifacts.

### Current limitations
- Installers are **not signed**: Windows needs a code-signing certificate, macOS needs an Apple Developer ID and notarization (the macOS build is ad-hoc signed).
- There is **no auto-update** yet. Adding it needs a stable URL for update files and `electron-updater`; use a URL you control so the storage can move later without breaking installed copies.
- The macOS build is new and has not been tested on a real Mac yet.
