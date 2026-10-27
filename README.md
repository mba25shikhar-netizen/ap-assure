# AP Assure app: free public version

Static app in `site/`, plus one serverless function (`netlify/functions/analyse.mjs`) that sends customer photos to Google Gemini. Anyone with the link can use it, no account needed. Hosting and the Gemini free tier cost nothing.

## Deploy on Netlify (about 5 minutes)
1. Get a free key: go to aistudio.google.com, sign in, choose Get API key, Create API key. No card is needed for the free tier.
2. Put this folder in a GitHub repo. In Netlify choose Add new site, Import from Git, pick the repo. Settings are read from `netlify.toml`.
   Alternative: install the Netlify CLI and run `netlify deploy --prod` inside this folder.
3. In Site settings, Environment variables, add `GEMINI_API_KEY` with your key. Redeploy.
4. Open the site on your phone. Upload a real damp photo. A live result says "Read by AI from your photos"; a canned one says it is a demo reading.

Optional variables: `GEMINI_MODEL` (default `gemini-2.5-flash`; if Google has retired it, pick a current Flash model that accepts images on the free tier) and `HOURLY_LIMIT_PER_IP` (default 12).

## Free-tier notes
- The free tier has per-minute and per-day request caps. If many jurors upload at the same moment, some analyses fail and the app falls back to a labelled demo reading. Check current limits on ai.google.dev/gemini-api/docs/pricing.
- On the free tier Google may use submitted content to improve its products. Use test photos, not photos of real customers' homes.
- The key lives only on the server. The per-IP limit is best effort.
- Cases are saved only in each user's own browser.
