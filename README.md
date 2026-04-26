# vercel-xhttp-relay
A minimal **Vercel Edge Function** that relays **XHTTP** traffic to your backend Xray/V2Ray server. Use Vercel's globally distributed edge network (and its `vercel.com` / `*.vercel.app` SNI) as a front for your real Xray endpoint — useful in regions where the backend host is blocked but Vercel is reachable.
