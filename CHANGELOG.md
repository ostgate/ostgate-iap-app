# Release notes

What is new in each version of Ostgate, newest first. The same notes, with what comes next,
are at [ostgate.app/changelog](https://ostgate.app/changelog).

## 0.0.9 — 11 November 2026

Apple Silicon · macOS 15 or later

- GKE stays responsive on large clusters. The Overview, the kind list and the tables are
  built off the main thread, an idle Overview no longer keeps the window busy, and a pod
  row's age or usage tick redraws only its own cells.
- Pods, Deployments and the other core kinds keep their watches when you switch kinds, so
  going back shows live rows at once.
- **GKE RECOMMENDATIONS** lists findings per workload, under the workload's name. Custom
  machine types such as `n2d-custom-16-32768` get a price, and the day's Billing Catalog is
  kept on the Mac across launches.
- A Logs tab keeps at most 64 MiB of text, so a stream of long lines no longer grows without
  limit.

Fixed: a namespace change shows "Loading pods…" until the new list arrives, sorts it at once
and keeps the Namespace column; Back and Forward work across namespaces; two windows on one
bastion-only cluster no longer end each other's link; a YAML tab reopens its link after the
Mac wakes; an account that must sign in again says so in the GKE and Resources lists.

## 0.0.8 — 10 November 2026

Apple Silicon · macOS 15 or later

- **GKE** gets its own sidebar area (⌘3) with the clusters of every pinned project of every
  signed-in account. Open a cluster to browse its pods, workloads, Services, Ingresses,
  Network Policies, ConfigMaps, Secrets, volumes, nodes, namespaces and events. CPU, memory
  and volume use come from Cloud Monitoring, with nothing installed in the cluster. Any
  object opens as read-only YAML; Secret values stay hidden until **Show**.
- Private clusters work through the DNS endpoint, the Connect gateway, a VPN or a bastion VM
  over IAP. **Diagnose Access…** names the setting that blocks a cluster and the gcloud
  command that fixes it.
- **Use with kubectl…** adds a cluster to `~/.kube/ostgate`, so kubectl, k9s and other tools
  sign in through Ostgate without gcloud or `gke-gcloud-auth-plugin`.
- Pod logs in a tab, **Show Logs (All Pods)** for a workload, **Forward Port…** on a pod or
  Service, **Open Shell…** in a container, **Restart…** and **Delete Pod…**. Each
  confirmation counts the pods that go down at once.
- The object inspector links related objects and lists what uses a ConfigMap or Secret. A
  cluster's Overview counts its security findings, **Open Cost** prices the cluster at list
  prices with rightsizing from 14 days of use, a pod's Workload Identity chain is checked link
  by link, and a Service, Ingress or Gateway shows its traffic path down to each pod.
- **Notify Me About Problems** on a cluster sends macOS notifications for crash loops,
  out-of-memory kills, stuck Pending pods, unhealthy nodes and stalled rollouts.
- **Cloud Shell** gets its own area (⌘4). Each account's Cloud Shell opens in a terminal tab
  with gcloud signed in as that account, and in a file browser. Connections, Local and
  Settings move to ⌘5, ⌘6 and ⌘7.
- A banner says when a newer Ostgate is out, and **Check for Updates…** asks on request.
  Ostgate never installs anything by itself.
- **Buy a License…** in the trial banner and in Settings › License opens the pricing page.
- Terminal tabs draw with Metal; **Draw with Metal** in Settings › Terminal turns it off.
- View › **Back** (⌘[) and **Forward** (⌘]), Quick Open over the open cluster's objects,
  Help › **Keyboard Shortcuts**, and a window that narrows to half a 13-inch screen with the
  inspector hidden.
- A tunnel or forward to port 80 is offered local port 8080, and Ostgate no longer offers a
  port that browsers refuse to open.
- The [privacy policy](https://ostgate.app/privacy) lists the new Google API calls. The OAuth
  scopes are the same as before.

Fixed: a tab's close button takes the first click, and opening a tab no longer shows the view
behind it for a moment.

## 0.0.7 — 29 October 2026

Apple Silicon · macOS 15 or later

- The welcome screen says why Google asks for access to Google Cloud, what each VM's
  project needs (a firewall rule from `35.235.240.0/20` and the Compute Viewer and
  IAP-secured Tunnel User roles), and that the 7-day trial needs no sign-up. It links to the
  IAP checklist.
- **Help › Setup Guide** opens the install and sign-in guide.
- When **Pin Project…** lists nothing, it says which case you are in: "No projects visible"
  when the account sees no projects, or "Project listing denied" when Google refuses the
  listing with HTTP 403. Each points to what to check.

Fixed: after Reconnect, an RDP tab's tooltip shows the time of the latest connect, and a
tab's × drops its hover highlight when it hides.

## 0.0.6 — 20 October 2026

Apple Silicon · macOS 15 or later

- Ostgate runs on macOS 15 Sequoia and 26.0 to 26.2. 0.0.5 and earlier needed
  macOS 26.3 or later.
- The × on a session tab highlights under the pointer.

## 0.0.5 — 18 October 2026

Apple Silicon · macOS 26.3 or later

- SSH connects to VMs that require OS Login certificates, where
  `enable-oslogin-certificates` is `TRUE`. Such a VM refused the key Ostgate imported with
  *Permission denied (publickey)*. Ostgate now has OS Login sign the key for that VM and logs
  in with the certificate, which Google issues for five minutes and Ostgate keeps in memory
  only. When your account has no POSIX account in the project yet, Ostgate creates it
  first. An RSA private key file of your own cannot be signed, and the SSH tab says so.
- Cloud SQL instances that have only a Private Service Connect address, as new instances in
  new projects now do, open a tunnel through their PSC endpoint. Ostgate looks for the
  endpoint in the instance's project and the consumer projects it allows, shows the
  endpoint's address in the Private IP column, and offers bastion VMs on the endpoint's
  network first. Without an endpoint the column reads "no endpoint" and **Open Tunnel…**
  says which projects it searched. The inspector also shows the instance's DNS name.
- The bastion picker in **Open Tunnel…** and **Open Proxy…** reloads your pinned projects'
  VMs when it opens, so a VM you started in the Cloud console is offered without a Refresh.
  When a project's VMs can't be listed, the picker shows the project and the error.
- The disk image opens as a window with Ostgate on the left, Applications on the right and
  an arrow between them.
- Remote Desktop runs on FreeRDP 3.32.2 and OpenSSL 3.6.5. They fix five FreeRDP advisories
  and CVE-2026-35189 in OpenSSL, which a malicious VM could trigger during an RDP session.

Fixed: a clicked row in Local Ports, Hosts and Connections keeps its accent tint and ↑ ↓
move from it, the sidebar's selected item stays gray, and a dragged column shows one sort
arrow.

## 0.0.4 — 12 October 2026

Apple Silicon · macOS 26.3 or later

### Menu bar

- The menu bar icon counts live and failed connections. Its panel lists them by account,
  failed first, each row with Copy, Stop, Diagnose and Retry. Below them are your open
  sessions and Quick Connect. Stopping a tunnel that has clients asks for confirmation
  inside the panel.

### Forwards on ports below 1024

- A forward can listen on a port below 1024, such as 443 or 22, so a web UI that redirects
  to its own host name, or an SSH clone URL, works without a port number. Such a forward
  needs a host alias with **Manage /etc/hosts aliases while running** on. Each alias gets
  its own loopback address between `127.0.0.2` and `127.0.0.254`, so two forwards can both
  use 443 under different aliases.
- The Ostgate port helper binds those ports. It runs as root, and macOS starts it only after
  you allow it once in System Settings › General › Login Items. On the first start of such a
  forward, Ostgate's own panel names the ports and what the helper does before macOS shows
  anything; Cancel installs nothing. After **Install and Open Login Items** the forward stays
  at Starting… for up to five minutes while you allow the helper, then starts. **Install**
  under **Settings › Connections › Port helper** also adds it, and **Remove** there takes it
  off.
- With the port helper installed, starting and stopping a forward with host aliases no
  longer asks for an administrator password. The helper writes and removes only Ostgate's
  own blocks in `/etc/hosts` and leaves every other line unchanged. Edits in
  **Local › Hosts**, aliases under names such as `googleapis.com` or `apple.com`, and macOS
  users who are not administrators still get the password prompt.

### Administrator password and /etc/hosts

- Before macOS asks for an administrator password, Ostgate shows a panel that says why:
  which forwards' aliases or how many Hosts edits it writes, or which port's process it
  stops. macOS 27 no longer shows that reason in its own dialog. Cancel in the panel never
  opens the macOS dialog.
- When a forward's alias is not written, because you cancelled or the write failed, the
  forward keeps listening and its row says so, for example "Hosts alias not written:
  cancelled", with **Retry**. At Quit, the password prompt names the forwards whose aliases
  it removes.
- Ostgate removes its loopback addresses and `/etc/hosts` entries when a forward stops and
  when you quit. After a crash, it removes them at the next launch.

### Connections and errors

- A forward through a bastion VM comes back sooner after a network drop. When the IAP relay
  leaves its reconnect unanswered for 60 seconds, the forward opens a new connection at
  once. In a Wi-Fi off and on test it served again 68 seconds after the network returned,
  where the previous build took 147 and 168 seconds. SSH tabs resume their session as before
  and keep their shell.
- Lists from Google Cloud retry by themselves, up to three more times, when Google answers
  429 or 503 (waiting as its Retry-After asks, up to 30 seconds) or the connection drops for
  a moment.
- Connection failures in forwards, SSH tabs and the Cloud Run proxy say what happened and
  what to do next, in place of the network library's own error text. A forward whose bastion
  VM is stopped says so before it dials: *The bastion VM "build-01" isn't running
  (TERMINATED). Start it, then try again.* Without a network, lists read "You're offline.
  Check your network connection, then refresh.", and error messages no longer show the
  request URL. A failed file operation is titled by what failed, such as
  **Couldn't delete "report.csv"**.

### Remote Desktop

- Keys and clicks reach Windows in the order you made them, without the wait of up to
  100 ms, so Shift-click and Ctrl-click select files as they do on a PC. Keys typed while
  the connection is down go out in order once it is back: with Wi-Fi off for 90 seconds, all
  169 lines typed into Notepad arrived unchanged. Windows highlights buttons and icons under
  the pointer, because pointer moves between clicks now reach it.

### Tables

- With 20,000 VMs, the Resources table re-sorts in less than half the time it took before,
  and scrolling stutters less while a refresh comes in. Cloud SQL and Cloud Run use the same
  table.
- Each window remembers its Resources column order, widths and hidden columns after you quit
  and reopen Ostgate. A new window opens with the default columns.
- In a table sorted by status, a VM whose status changes keeps its place while the pointer
  is over the table, a menu is open or the row is selected. It moves when the pointer leaves
  or you refresh. Cloud SQL and Cloud Run tables do the same.
- A selected row has a light tint instead of a solid fill, and the column header no longer
  sits on its own band.

### Confirmations and details

- Confirmations show the account, the project and its environment, such as PROD or STAGING:
  Stop, Start and Unpin on a VM, Stop on a tunnel, Delete and Replace in Files, and deleting
  an SSH key.
- SSH Keys and the Event Log show a spinner while they first load. A value cut short in the
  inspector shows in full when you hold the pointer over it.

Fixed: a tunnel name that already carries its port no longer shows it twice, a reconnect
that gets no answer from the relay for 60 seconds dials again, a failed SSH connection
closes its socket at once, and the port helper checks every request more strictly.

## 0.0.3 — 8 October 2026

Apple Silicon · macOS 26.3 or later

- Fixed: on macOS 26, Ostgate quit as soon as a Remote Desktop connection started.

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
