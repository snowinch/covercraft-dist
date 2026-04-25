# 💿 CoverCraft Distribution & Releases

This repository serves as the official distribution channel and update server for **CoverCraft**. It hosts the compiled binaries, release manifests, and assets required for the application's auto-update functionality.

The source code for the application can be found at: [snowinch/covercraft](https://github.com/snowinch/covercraft).

[![Latest Release](https://img.shields.io/github/v/release/snowinch/covercraft-dist?style=for-the-badge&color=7dd3fc)](https://github.com/snowinch/covercraft-dist/releases/latest)
[![Platform Support](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-lightgrey?style=for-the-badge)](#)

---

## 🚀 Download & Installation

You can always find the latest stable version in the **[Releases](https://github.com/snowinch/covercraft-dist/releases/latest)** section.

### 🪟 Windows
1. Download the `.exe` installer (NSIS).
2. Run the installer. The application will install to your local user directory and launch automatically.

### 🍎 macOS
1. Download the `.dmg` file.
2. Open the disk image and drag **CoverCraft** to your *Applications* folder.
3. **Note for macOS Users:** If the application is not signed with an Apple Developer certificate, you may need to right-click the app icon and select "Open" to bypass macOS Gatekeeper (security check) for the first time.

---

## 🔄 How Auto-Updates Work

This repository acts as a static update server. The CoverCraft application integrates `electron-updater` to monitor this repository for changes.

### The Update Logic:
On startup, the application fetches and compares its local version with the manifest files hosted here:
* **`latest.yml`**: Contains metadata for the latest **Windows** version (version number, SHA-512 hash, and release date).
* **`latest-mac.yml`**: Contains metadata for the latest **macOS** version.

If a newer version is detected, the app downloads the update in the background and prompts the user to restart and apply the changes.

---

## 🛠 Technical Details (DevOps)

### Automated Release Workflow
Releases in this repository are fully automated via GitHub Actions triggered from the main [covercraft](https://github.com/snowinch/covercraft) repository.

1.  **Trigger:** A push to the `main` branch.
2.  **Build:** GitHub Actions builds the production assets for both Windows (NSIS) and macOS (DMG).
3.  **Deployment:** Using a Personal Access Token (PAT), `electron-builder` uploads the following files to this repository:
    * `.exe` / `.dmg`: The primary installers.
    * `.blockmap` files: Used for "differential updates" to reduce download size.
    * `.yml` files: The update manifests.

### Auto-Updater Configuration (Client-Side)
The application is configured to point to this repository via the `publish` block in `package.json`:

```json
"publish": {
  "provider": "github",
  "owner": "snowinch",
  "repo": "covercraft-dist"
}
```

---

## ⚠️ Troubleshooting

* **Update Not Triggering:** Ensure your local version is lower than the version specified in the `latest.yml` file in this repository. 
* **Checksum Mismatch:** If an update fails to verify, it may be due to a corrupted upload. Please download the latest version manually from the Releases page.
* **macOS "App Damaged" Error:** This is often a result of Gatekeeper blocking an unsigned app. Please follow the "right-click -> Open" method mentioned in the installation section.

---

## 📄 License

The binaries distributed here are subject to the same license as the [CoverCraft source code](https://github.com/snowinch/covercraft).

---
**Maintained by [snowinch](https://github.com/snowinch)**
