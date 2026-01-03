# Plane Caddy Proxy (Fixed)

This is a fixed version of the Railway Plane Caddy proxy that includes the **missing `/live/*` route** for WebSocket collaboration (Pages editor).

## The Fix

The original template at `railwayapp-templates/plane-caddy-proxy` is missing the `/live/*` route, which causes the Pages editor to fail because WebSocket connections to the Live service aren't being proxied.

This fix adds:
```
handle /live/* {
    reverse_proxy {$LIVE_ENDPOINT} {
        header_up Host {upstream_hostport}
    }
}
```

## How to Use

1. Push this repo to your GitHub
2. In Railway Dashboard, go to the **Plane** (proxy) service
3. Go to **Settings** → **Source**
4. Change the source to your GitHub repo

## Required Environment Variables

The Plane proxy service should already have these configured:
- `LIVE_ENDPOINT` - e.g., `http://live.railway.internal:3000`
- `WEB_ENDPOINT`
- `ADMIN_ENDPOINT`
- `API_ENDPOINT`
- `SPACES_ENDPOINT`
- `BUCKET_ENDPOINT`
- `BUCKET_NAME`
