# Release notes

What is new in each version of Ostgate, newest first. The same notes, with what comes next,
are at [ostgate.app/changelog](https://ostgate.app/changelog).

## 0.0.2 — 7 October 2026

Apple Silicon · macOS 26.3 or later

### Window and sessions

- Accounts sit in a rail on the left, each with a badge for its open problems. `⌥⌘1…9`
  switches between them, and the sidebar collapses to icons.
- SSH and Remote Desktop tabs carry a session bar: status, account, `user@vm`, address,
  route and **Disconnect**.
- Short confirmations appear as toasts over the window: a refresh, a copied address, a
  closed tab.

### Files

- Upload whole folders with Upload… or by dragging them in. A folder that already exists on
  the instance is merged after one confirmation for the whole upload.
- Download a folder, several files, or folders and files together as one ZIP, built on your
  Mac.
- A folder, or five or more items, is packed on the instance with `tar` and streamed
  compressed over the same connection, with nothing written to its disk. A folder of 5,000
  small files takes a few seconds. SFTP-only logins copy several files at a time.
- A Files tab that loses its connection shows **Connection lost** with **Reconnect**, which
  brings it back in the same folder.

### Accounts

- Without a network an account shows **can't be reached** with **Check Again**, and is
  checked again by itself when the network returns.
- Sign-ins or SSH keys left in the Keychain by an account that is no longer in Ostgate are
  listed under **Review…**, to remove or restore.

### Tunnels and forwards

- Tunnels ride out relay drops, Wi-Fi outages and sleep: they dial again as soon as the
  network returns or the Mac wakes. A tunnel that can't come back says so within a few
  minutes, with **Reconnect**.
- New Tunnel… has an **Interface** row for instances with more than one network interface.
- When a tunnel's or forward's access setting turns a program away, the row names the
  program, and **Change Access…** lets it in.
- Local Ports names the ports Ostgate itself listens on.
- Cloud SQL **Via bastion** lists the Linux VMs on the instance's network first.

### Remote Desktop

- After you log on with a typed password, the bar over the desktop offers to save it.
- The shared folder is a per-instance connection setting; **Share Folder…** in the Session
  menu changes it and reconnects.
- **Set Windows Password…** asks first, naming the account and project, and fills in the
  Windows user set for that instance.

### SSH

- `ssh` from Terminal tries each signed-in account in turn, starting with those that have
  the instance's project pinned, until one is allowed through.

### Settings and licence

- Settings is split into tabs: Connections, Accounts, SSH, Terminal and License.
- License shows how many Macs your plan covers, and **Manage Subscription…** opens your
  subscription. **Enter New Key…** switches a licensed Mac to another key.
- A renewed licence takes effect without entering the key again.

Plus fixes, security hardening and polish throughout.

## 0.0.1 — 30 September 2026

The first release: SSH, Remote Desktop, SFTP and TCP tunnels to Compute Engine VMs through
IAP, several Google accounts side by side, Cloud SQL and Cloud Run tunnels, Terminal
integration and the Connection Doctor. Full notes:
[ostgate.app/changelog#v0.0.1](https://ostgate.app/changelog#v0.0.1).
