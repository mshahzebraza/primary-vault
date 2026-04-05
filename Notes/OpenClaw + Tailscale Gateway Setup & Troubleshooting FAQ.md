---
original_path: "Notes/Tech Learning/OpenClaw/OpenClaw + Tailscale Gateway Setup & Troubleshooting FAQ.md"
base: TechLearning
path_area: OpenClaw
categories:
  - "[[TechLearning]]"
  - "[[OpenClaw]]"
---
## 1. Network Connectivity (The "Site Can't Be Reached" Error)
* **The Problem**: Accessing `127.0.0.1:18789` directly from a local device fails because the Gateway is bound to the VPS loopback.
* **Verification**
	* `openclaw config set gateway.bind` returns `loopback` (means gateway is running on `localhost:18789` on the vps)
	* `openclaw confit get gateway.auth.allowTailscale` returns `true` (If tailscale connection is required)
	* `openclaw config get gateway.tailscale.mode` returns `serve` (If tailscale connection is required. `funnel` is also valid but less secure)
	* Visit the url provided by `openclaw status | grep Tailscale` to view the tailscale magic url
	* Get the local gateway url by visiting `openclaw dashboard`
* **The Fix**: Use **Tailscale Serve** to map the local port to your Tailnet DNS.
* **Recommended way**:
	  - run the `openclaw onboard` or `openclaw configure` or `openclaw config`.
* **Manual Tailscale serve verification**:  
    * Run `tailscale serve status` on the VPS.
    * Confirm mapping: `https://[vps-name].[tailnet-id].ts.net -> http://127.0.0.1:18789`.

## 2. Security Handshake (The "Allowed Origins" Error)
* **The Problem**: OpenClaw blocks UI requests from domains not explicitly "paired" in the config.
* **The Fix**: Add your `https://kvm....ts.net` URL to `~/.openclaw/openclaw.json` manually:
```json
"controlUi": {
  "allowedOrigins": [
	"http://localhost:18789",
	"[https://kvm-vps-srv1349367.taild477fa.ts.net](https://kvm-vps-srv1349367.taild477fa.ts.net)"
  ]
}
```
* **Alternative**: Use `openclaw config set gateway.controlUi.dangerouslyAllowHostHeaderOriginFallback true` to trust the proxy host.

## 3. Authentication Sync (The "Stale Token" Warning)
* **The Problem**: The `systemd` service runs with the token present at the time of installation, creating a mismatch if the JSON token is changed later.
* **The Fix**: Sync the service environment with:
```bash
openclaw gateway install --force
```
    *Note: Follow this with `systemctl --user restart openclaw-gateway`*.
- Or reinstall using the `onboard` or `configure` cli

## 4. Device Pairing (The "Pairing Required" Dashboard)
* **The Problem**: New browsers/devices are marked as "Pending" until an admin approves the unique Request ID.
* **The Fix**:
    1.  Get the ID from the UI or run `openclaw devices list`.
    2.  Approve the ID:
```bash
openclaw devices approve <requestId>
```
* **Verification**: Dashboard status changes from **Offline** to **Online**.

---

## Quick Reference Commands
* **Check Health**: `openclaw gateway status` (RPC probe should be `ok`).
* **Deep Probe**: `openclaw gateway probe`.
* **Logs**: `tail -f /tmp/openclaw/openclaw-$(date +%Y-%m-%d).log`.