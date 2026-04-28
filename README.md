# vercel-xhttp-rewrite-only

Function-free Vercel external rewrite relay.

This variant removes `api/index.js` entirely and uses Vercel external rewrites, so it should avoid Fluid Compute, Function Invocation, Fluid Active CPU, and Fluid Provisioned Memory charges. You will still pay for edge/origin transfer, edge requests, observability, and any other platform-level usage.

## Configure

Edit `vercel.json`:

- Replace `YOUR_SECRET_PATH` with the exact path your client uses, for example `xhttp-a8f2c9`.
- Replace `https://YOUR_TARGET_DOMAIN` with your origin, for example `https://origin.example.com:2096`.

If your Vercel path and origin path are different, use this pattern instead:

```json
{
  "source": "/YOUR_VERCEL_SECRET_PATH/:path*",
  "destination": "https://YOUR_TARGET_DOMAIN/YOUR_ORIGIN_XHTTP_PATH/:path*"
}
```

## Deploy

```bash
npm i -g vercel
vercel login
vercel --prod
```

## Test

```bash
curl -i https://YOUR_PROJECT.vercel.app/YOUR_SECRET_PATH
```

Then point your XHTTP client at the Vercel domain and the same path you configured as the rewrite source.

## Important

External rewrites are not the same as your previous Edge Function. They do not run custom JavaScript, so you cannot strip headers, modify `x-forwarded-for`, or use custom request handling. Test XHTTP behavior before relying on it.
