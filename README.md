# MATLAB Distrobox Environment

An automated, portable setup for running MATLAB via the MathWorks Package Manager (MPM) inside an isolated Ubuntu 24.04 Distrobox container. 

This architecture is explicitly designed for immutable operating systems (like NixOS) and Btrfs snapshot workflows (like Snapper). By keeping the container home and application binaries in a dedicated persistent subvolume, it prevents multi-gigabyte MATLAB toolboxes from polluting your root directory or bloating your system rollbacks.

## Features
* **Isolated Footprint:** Installs MATLAB into a custom `--home` and mounted `/opt/apps` volume, keeping host dotfiles and system snapshots perfectly clean.
* **Modern Authentication:** Uses `mpm` to bypass legacy license files, allowing you to activate MATLAB via web browser SSO (Campus-Wide Licenses).
* **Wayland & X11 Ready:** Automatically configures graphical environment variables to ensure the modern Chromium-based MATLAB desktop runs smoothly.
* **Host Integration:** Generates a dynamic wrapper script and a native `.desktop` entry so MATLAB feels like a locally installed host application.

## Prerequisites
* Linux host environment (NixOS, Fedora Silverblue/Kinoite, Arch, Ubuntu, etc.)
* [Distrobox](https://github.com/89luca89/distrobox) installed.
* Podman or Docker installed.

## Setup Instructions

1. **Clone the repository:**
```bash
git clone [https://github.com/hkn-alp/matlab-distrobox.git](https://github.com/hkn-alp/matlab-distrobox.git)
cd matlab-distrobox

```

2. **Configure your Toolboxes:**
Open `mpm-input-r2026a.txt` and uncomment the specific toolboxes you need (e.g., `product.Aerospace_Toolbox`, `product.Optimization_Toolbox`).
3. **Run the Installer:**
Make the script executable and run it:

```bash
chmod +x setup-matlab.sh
./setup-matlab.sh

```

*The script will ask if you want to run `mpm install` immediately. Press `y` and it will automatically use the `mpm-input-r2026a.txt` file included in the repository.*

4. **Authenticate:**
Once installed, launch MATLAB from your host desktop application grid or via the terminal wrapper. MATLAB will display an authentication link or open your host web browser automatically. Log in with your university/MathWorks credentials to activate your local session.

## File Structure

* `setup-matlab.sh`: The core deployment script. Handles dependencies, container creation, and host integration.
* `mpm-input-r2026a.txt`: The configuration file dictating which products and toolboxes `mpm` will download. Safe to share publicly (contains no keys or personal data).

## Future Roadmap

* General Mission Analysis Tool (GMAT) container integration.
