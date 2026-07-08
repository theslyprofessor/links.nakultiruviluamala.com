# links.nakultiruviluamala.com

Self-hosted LittleLink-style link-in-bio page. Static Astro → nginx → Dokploy + Traefik.
Mirrors the deploy pattern of the other `.com` sites in this org.

## Edit your links

All content lives in **`src/data/links.json`** — no code changes needed.

```jsonc
{
  "profile": { "name": "...", "tagline": "...", "avatar": "/avatar.jpg" },
  "links": [
    { "label": "YouTube", "url": "https://youtube.com/@you", "brand": "youtube" }
  ]
}
```

`brand` picks the button color from the `BRANDS` map in `src/pages/index.astro`.
Supported out of the box: youtube, soundcloud, instagram, spotify, applemusic,
bandcamp, tiktok, twitter, facebook, patreon, website. Add more by adding a row
to `BRANDS`. Unknown brand falls back to a neutral dark button.

Avatar: drop `public/avatar.jpg` (square, ~400px). Missing avatar hides itself.

## Click analytics (optional)

Set `PUBLIC_POSTHOG_KEY` (your PostHog **public** `phc_...` project key) at build
time. Each button click fires a `link_click` event with `{ label, url }`.
Without the key, tracking is a no-op — page still works.

## Local dev

```bash
bun install
bun run dev      # http://localhost:4337
bun run build    # → dist/
```

## Deploy (Dokploy)

New Compose service in Dokploy pointing at this repo, compose file
`docker-compose.prod.yml`. Point DNS `links.nakultiruviluamala.com` →
the Dokploy VPS, Traefik issues the LE cert automatically.
