
<div align="center">

# OryvexG2ray

A sleek **web dashboard** for managing Xray VLESS xHTTP configs on GitHub Codespaces.

</div>

---

<br>

## Overview

OryvexG2ray is a powerful, interactive **web panel dashboard** designed to instantly deploy and manage Xray VLESS xHTTP configurations. Built specifically for the GitHub Codespaces environment, it automatically generates ready-to-use configs with multiple IP support.

Once the Python backend starts, it serves a full dashboard on the forwarded Codespaces web port. From there, you can manage clients, preview generated configs, copy subscription links, view logs, monitor traffic, and control Xray core.

> **Note:** The panel includes an optional background wake-lock/keepalive feature to help keep the Codespace active while the proxy is in use. Use this feature at your own risk and follow GitHub Codespaces policies.

---

## Core Features

### Web Dashboard Control Panel

Manage everything from a clean browser UI instead of a terminal/curses interface. Create clients, edit limits, view QR codes, copy subscription links, restart Xray, and monitor the system from one dashboard.

### VLESS xHTTP Config Generation

Generate VLESS xHTTP client links and subscription outputs for GitHub Codespaces forwarding domains. The panel is designed around modern Xray clients and avoids deprecated insecure TLS options.

### Live Analytics & Quota

Tracks real-time RX/TX data consumption, connection status, Xray uptime, CPU/RAM usage, disk usage, and estimated Codespaces free-tier quota.

### Subscription Lab

Build custom per-client subscription layouts directly in the web panel. Add proxy entries, info entries, placeholders, custom names, usage indicators, and live mobile-style previews.

### Optional Wake Lock / Keepalive

Includes optional controls for keeping the runtime active while the service is in use. This can be toggled from the web dashboard.

### Multiple IP Support

Add multiple proxy entries with different IP addresses in the Subscription Lab for load balancing and redundancy.

---

## Quick Start

### 1. GitHub Codespaces (Browser / VS Code)

*No local installation required.*

1. **Fork the Repository**: Click **Fork** at the top-right of this GitHub page.
2. **Create a Codespace**: Open your fork, click the green **Code** button, go to **Codespaces** tab, and click **Create codespace on main**.
3. **Wait for Environment**: Allow 1-2 minutes for the container to build.
4. **Launch Backend**: The `oryvex_g2ray.py` backend should start automatically in the integrated VS Code terminal.
5. **Open Web Dashboard**: Open the forwarded web port URL printed in the terminal. It will look similar to:

   ```text
   https://<your-codespace-name>-8080.app.github.dev/
   ```

---

## Usage

When launched, the backend prints your dashboard and Xray forwarding URLs in the terminal.

```bash
# If the backend does not start automatically for any reason, run:
python3 oryvex_g2ray.py
```

Then open the dashboard URL in your browser:

```text
https://<your-codespace-name>-8080.app.github.dev/
```

Inside the web dashboard, you can:

- View live traffic, speed, uptime, and hardware usage from **Dashboard**.
- Manage Codespaces region/IP/quota details from **Codespace Settings**.
- Create, edit, enable, disable, delete, and QR-share clients from **Client Profiles**.
- Build custom per-client subscriptions from **Subscription Lab**.
- Configure routing, DNS, sniffing, logging, and core options from **Advanced Settings**.
- View Xray and panel logs from **Console Logs**.

> Opening the Xray forwarded port directly in a browser may show `400`. That is normal for VLESS xHTTP. Use the generated VLESS or subscription link in a compatible client instead.

---

## Architecture

```mermaid
graph LR
    A[GitHub Codespace] -->|Runs| B[OryvexG2ray Python Backend]
    B -->|Serves Web UI on 8080| C[Browser Dashboard]
    B -->|Generates Config| D[Xray-core]
    D -->|Binds Port 443| E[Codespace App Domain]
    E -->|VLESS over xHTTP| F[End User Client]
```

<details>

<summary><kbd>Project Structure</kbd></summary>

```text
OryvexG2ray/
├── data/                    # Dynamic storage for usage stats, UUIDs, panel state, and configs
├── logs/                    # Xray and panel logs
├── assets/                  # Media resources, previews, and videos
└── oryvex_g2ray.py          # Python backend, web dashboard server, and Xray manager
```

</details>

---

<details>

<summary><kbd>FAQ</kbd></summary>

### Is this still a TUI/curses panel?

No. Current versions use a **web panel dashboard**. The terminal is only used to start the Python backend and print the dashboard URL.

### Where do I open the panel?

Open the forwarded web port, usually:

```text
https://<your-codespace-name>-8080.app.github.dev/
```

### Why do I see HTTP 404 on port 443?

That is expected. Port `443` is used by Xray VLESS xHTTP, not the web dashboard. Browsers send normal HTTP requests, while Xray expects xHTTP proxy traffic. Use the generated config in your V2ray/Xray client.

### My Codespace keeps shutting down. What can I do?

Open **Codespace Settings** in the dashboard and enable the optional wake-lock feature if you understand the risks. Make sure your usage complies with GitHub Codespaces policies.

### Why are my speeds slow?

For optimal routing, try setting your GitHub Codespace region to a nearby or well-connected region such as Europe West in your GitHub account settings.

</details>

<br>

<div align="center">

> **Educational Purpose Only:** This project is provided for educational and research purposes. Users are solely responsible for compliance with all local laws. The developer assumes no liability for misuse.



</div>
