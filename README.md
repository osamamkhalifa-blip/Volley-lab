# Volley Lab

A brick-breaker that tracks how hard each ball works. Installs to an iPhone or iPad home screen and runs offline.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole game |
| `sw.js` | Service worker that caches the game for offline play |
| `manifest.webmanifest` | App name, colors and icons for the home screen |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | Icons |

iOS only installs and caches the app when it is served over **HTTPS**, so pick one of these hosts.

## Option A: GitHub Pages (free, about 5 minutes)

1. On github.com, create a new public repository named `volley-lab`.
2. Click **Add file → Upload files**, drag in every file from this folder, and commit.
3. Go to **Settings → Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
4. After about a minute the site is live at `https://<your-username>.github.io/volley-lab/`.

## Option B: Your home server

Serve the folder from any static web server that has HTTPS. For example, Caddy in a Proxmox LXC:

```
volley.example.com {
    root * /srv/volley-lab
    file_server
}
```

Caddy gets the certificate for you. If the server only runs on your home network, you need a real certificate (for example from a Cloudflare Tunnel or Tailscale `serve`). A self-signed certificate won't let iOS install the app.

## Install on iPhone or iPad

1. Open the URL in **Safari**.
2. Tap **Share → Add to Home Screen → Add**.
3. Launch it from the home screen icon. It opens full screen and works offline after the first load.

Each device keeps its own stats. To move them, open **Lifetime → Export stats** on the old device, then **Import stats** on the new one.

## Updating

Replace `index.html` and change the version in the first line of `sw.js` (for example `volley-lab-v4` → `volley-lab-v5`). Installed copies pick up the update the next time they open while online. Stats are kept.

Removing the home screen app, or clearing Safari website data, erases the stats on that device. Export first.
