# Euro Truck Simulator 2 - Custom AMP Template

> **Status:**
> - **Euro Truck Simulator 2** — Work in progress. Expect issues and incomplete features.
> - **American Truck Simulator** — Not yet tested. Use at your own risk.

A custom AMP (Application Management Panel) Generic Module template for running
a Euro Truck Simulator 2 dedicated convoy server.

---

## Files

| File | Purpose |
|------|---------|
| `euro-truck-simulator-2.kvp` | Main AMP instance configuration |
| `euro-truck-simulator-2config.json` | Settings manifest (AMP UI fields) |
| `euro-truck-simulator-2metaconfig.json` | Maps UI settings to the server config file |
| `euro-truck-simulator-2ports.json` | Port definitions |
| `euro-truck-simulator-2updates.json` | SteamCMD download stages |
| `euro-truck-simulator-2.sii` | Server config template (do not edit directly — AMP manages this) |

---

## Prerequisites

1. **AMP installed** — https://cubecoders.com/AMP
2. **Docker** (required on Windows, optional on Linux) — https://www.docker.com/
3. **Steam Game Server Login Token (GSLT)** — Required for your server to appear
   in the public server browser.
   - Go to: https://steamcommunity.com/dev/managegameservers
   - Use **App ID `227300`** (ETS2 client)
   - Generate a token and copy it — you'll paste it into AMP under
     "Server Logon Token".

---

## How to Add This Template to AMP

### Option A — Use the Official Template (Simplest)

ETS2 is already in the official CubeCoders template repository. In AMP:

1. Go to **ADS → Configuration → Instance Deployment**.
2. Under "Configuration Repositories", ensure `CubeCoders/AMPTemplates` is listed
   (it should be there by default).
3. Click **Fetch** to refresh.
4. Create a new instance and search for **Euro Truck Simulator 2**.

### Option B — Use This Custom Template

1. **Host the files** — Upload this folder to a public GitHub repository.
   Example: `yourusername/ets2-amp-template`

2. **Point AMP to your repo** — In AMP:
   - Go to **ADS → Configuration → Instance Deployment**
   - Click **Add** under Configuration Repositories
   - Enter: `yourusername/ets2-amp-template:main`
   - Click **Fetch**, then refresh the browser.

3. **Create the instance** — Click **Create Instance**, search for your template.

### Option C — Manual Local Install

Place all `.kvp`, `.json`, and `.sii` files directly into:

- **Windows:** `C:\AMP\datastore\`
- **Linux:** `/home/amp/.ampdata/datastore/` (or your AMP data path)

Then in AMP, create a Generic Module instance and point it to the `.kvp` file.

---

## Server Setup Steps

1. **Create the AMP instance** using the template.
2. **Run the update** (click Update in AMP) — this downloads the ETS2 dedicated
   server via SteamCMD (~2 GB).
3. **Generate server packages** *(required — server will not start without this)*
   - Launch **Euro Truck Simulator 2** on your own PC (the regular game client).
   - Open the in-game developer console (press `~` or `` ` ``).
   - Run the command: `export_server_packages`
   - This creates two files in your local ETS2 documents folder
     (`Documents\Euro Truck Simulator 2\`):
     - `server_packages.sii`
     - `server_packages.dat`
   - Copy **both files** into the server's home directory inside the AMP instance:
     `<AMP datastore>\<instance>\euro-truck-simulator-2\1948160\Euro Truck Simulator 2\`
   - These files tell the server which map, DLCs, and mods to use. If you add or
     remove DLCs/mods later, you must repeat this step.
4. **Configure your server** in AMP's settings panel:
   - Set your **Lobby Name**, **Description**, **Welcome Message**
   - Set a **Password** (optional, leave blank for public)
   - Paste your **Server Logon Token**
   - Adjust gameplay options as desired
5. **Forward ports** in your router/firewall:
   - **UDP 27015** — Main game port
   - **UDP 27016** — Steam query port
6. **Start the instance** — click Start in AMP.

---

## Ports

| Port | Protocol | Purpose |
|------|----------|---------|
| 27015 | UDP | Main game traffic |
| 27016 | UDP | Steam server query |

---

## Notes

- The server requires a valid **Steam Game Server Login Token** to show in the
  server browser. Without it, the server runs but is unlisted.
- On **Windows**, AMP can run this server natively. Docker is optional but supported.
- The actual server config is written to:
  `Euro Truck Simulator 2/server_config.sii` inside the instance directory.
  AMP manages this automatically — do not edit it manually.
- The server binary is at: `1948160/bin/linux_x64/eurotrucks2_server` (Linux)
- SteamCMD App ID: **1948160** (server), Client App ID: **227300**

---

## Steam Server Login Token

1. Visit https://steamcommunity.com/dev/managegameservers
2. Log in with your Steam account
3. Enter App ID: `227300`
4. Enter a memo (e.g., "ETS2 Server")
5. Click **Create**
6. Copy the token and paste it into AMP's **Server Logon Token** field

---

## Useful Links

- [ETS2 Dedicated Server Guide](https://steamcommunity.com/app/227300/discussions/)
- [AMP Documentation](https://github.com/CubeCoders/AMP/wiki)
- [AMP Generic Module Config Guide](https://github.com/CubeCoders/AMP/wiki/Configuring-the-%27Generic%27-AMP-module)
- [CubeCoders AMPTemplates Repo](https://github.com/CubeCoders/AMPTemplates)
- [AMP Community Discord](https://discord.gg/cubecoders)
