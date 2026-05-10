# Windrose Dedicated Server AMP template

This repository contains a Generic Module template for **Windrose Dedicated Server** on AMP.

## What this template assumes

- Dedicated server Tool App ID: `4129620`
- Parent game App ID: `3041230`
- Steam install dir: `Windrose Dedicated Server`
- Launch command: `WindroseServer.exe -log`
- On Linux, AMP runs the Windows server through **Proton**
- The game guide says ports are **dynamically assigned via NAT punch-through**, so this template does **not** expose fixed AMP ports

## Files in this repo

- `manifest.json`
- `windrose.kvp`
- `windroseconfig.json`
- `windrosemetaconfig.json`
- `windroseports.json`
- `windroseupdates.json`

## Before you publish

Edit `manifest.json` so these values are unique to your repository:

- `id`
- `origin`
- `url`
- `prefix`

If you plan to open a pull request against the official `CubeCoders/AMPTemplates` repository later, revert or exclude your manifest changes first.

## Deploy to GitHub

### Option A: create a fresh repository

1. Create a new GitHub repository.
2. Upload all files from this folder into the **repo root**.
3. Commit and push.

### Option B: fork AMPTemplates

1. Fork `CubeCoders/AMPTemplates`.
2. Place these files in the **repo root** of your fork.
3. Edit `manifest.json`.
4. Commit and push to your branch.

## Add the repo to AMP

In AMP:

1. Go to **Configuration -> Instance Deployment**.
2. Click **Add Configuration Repository**.
3. Enter the repo in the format:

   `owner/repo:branch`

   Example:

   `yourname/windrose-amp-template:main`

4. Click **Fetch**.
5. Refresh the browser.
6. Create a new instance and pick the template with your manifest prefix.

## First boot workflow

The Windrose guide says `ServerDescription.json` and world files are auto-created on the first launch.

Because of that, do this after creating the instance:

1. Start the server once.
2. Wait for it to finish initial setup.
3. Stop the server.
4. Open the AMP configuration editor and adjust the generated `ServerDescription.json` settings.
5. Start the server again.

The server config file used by AMP is:

`4129620/R5/ServerDescription.json`

## Networking note

The public guide says Windrose uses **dynamic NAT punch-through** and that you **cannot manually specify fixed server ports**.

You should therefore:

- enable **UPnP** or NAT punching on the host router
- avoid VPNs and proxies on the server host
- treat the template's lack of fixed AMP ports as intentional

## Linux note

On Linux hosts, the template downloads the Windows dedicated server build and a Proton runtime via SteamCMD.

## Caveat

The ready regex is a best-effort match based on the guide saying the console shows an invite code when the server is loaded. If the instance starts correctly but AMP never flips to ready, adjust `Console.AppReadyRegex` in `windrose.kvp` to match the real startup log line you see on your system.
