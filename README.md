# AM HMS releases

Public Windows installers, automatic update metadata, and the Linux Mint hotspot preview for AM HMS. Source is maintained in the private am-hms repository.

## Linux Mint 22.3 Xfce installation

The Linux preview lets the server computer provide its own Wi-Fi hotspot, DHCP and local DNS. Phones join **HMS** Wi-Fi and open **http://hms.home.arpa**. No router or manual phone DNS/IP configuration is required for clients using normal DHCP settings.

Download: [Linux Mint hotspot preview 0.1.19](https://github.com/MohamedFadlala/am-hms-releases/releases/tag/linux-v0.1.19).

### Requirements

- Linux Mint **22.3 Xfce, 64-bit (x86_64)**.
- A USB Wi-Fi adapter whose Linux driver supports **access-point (AP) mode**. Connect it before installation; the installer checks compatibility.
- A normal desktop user with sudo access.
- Internet access for the initial installation. Normal HMS hotspot operation works offline.

Run installation from a terminal on the server itself. The selected Wi-Fi adapter will disconnect from its current network when it switches to hotspot mode.

### Install with one command

Run this as your **normal desktop user**, not from a root shell:

```bash
sudo apt-get update && sudo apt-get install -y curl && curl -fL https://github.com/MohamedFadlala/am-hms-releases/releases/download/linux-v0.1.19/install-mint.sh -o /tmp/hms-install.sh && bash /tmp/hms-install.sh
```

The installer:

1. Requests administrator access and installs the required packages.
2. Downloads the Linux bundle and verifies its SHA-256 checksum.
3. Asks which Wi-Fi adapter to use if multiple compatible adapters are found.
4. Prompts twice for a new **HMS** Wi-Fi password.
5. Configures the hotspot, automatic DHCP, local DNS, firewall rules and desktop startup.
6. Starts HMS as your normal user.

This preview installer refuses to overwrite an existing HMS installation.

### Connect Android and iPhone

1. Complete HMS activation or explicitly start the trial on the server. Create the administrator account if this is a new installation.
2. On Android or iPhone, connect to **HMS** Wi-Fi using the password you chose.
3. If the phone reports that the Wi-Fi has no internet, choose to remain connected.
4. Open **http://hms.home.arpa** in Android Chrome or iPhone Safari and sign in.

No QR code is needed. Use the complete `http://` address. Opera Mini's remote compression mode is unsuitable for the offline application.

The fallback address is **http://10.42.0.1**. The hotspot address stays fixed even when an upstream Ethernet or internet connection receives a different IP.

### Startup and verification

The hotspot starts at boot. **HMS starts after the designated user signs into the Mint desktop**, with the keyring available. This is not a pre-login service. Keep the server awake during operating hours.

After installation:

- Confirm both phones can open the app, sign in and receive live updates.
- Disconnect upstream internet and repeat the tests.
- Restart Mint, sign into the usual desktop account, and confirm HMS starts without launching it manually.
- Reconnect the USB Wi-Fi adapter and repeat the phone tests.

If the hostname fails but `http://10.42.0.1` works, check the phone's DNS/VPN policy. Strict custom Private DNS, VPNs or proxy browsers can override the DNS supplied by the hotspot. The server cannot override every client policy.

### Preview status

Built using [GitHub Actions](https://github.com/MohamedFadlala/am-hms/actions/runs/42720967487). Automated tests, packaged Linux runtime checks, checksums and public download verification passed. Physical testing on your Mint installation, USB adapter, Android phone and iPhone remains required. The source workflow is in the private repository.

HMS uses HTTP only; credentials and patient data are not encrypted in transit. Authentication and role restrictions remain enforced. Existing Windows hardware-bound activation does not automatically transfer to Linux.

## Windows

Windows installers and their automatic update metadata remain available under [Releases](https://github.com/MohamedFadlala/am-hms-releases/releases). The Linux preview is a separate prerelease and does not replace the Windows stable update feed.
