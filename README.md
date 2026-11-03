# Deployment

## Google Maps API keys

For local deployment, copy `.env.example` to `.env` and set both Google Maps API
keys:

```powershell
Copy-Item .env.example .env
```

`docker compose` loads `.env` automatically when run from this directory. The
`.env` file is ignored by Git and must not be committed. For deployments through
GitHub Actions, configure the `GOOGLE_MAPS_API_KEY` and
`GOOGLE_MAPS_BROWSER_KEY` repository secrets.