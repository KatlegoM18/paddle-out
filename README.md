   # Paddle Out: live beach and surf conditions for South Africa

**Live demo:** [cornerstonetechdev.co.za/projects/paddle-out](https://cornerstonetechdev.co.za/projects/paddle-out/)

## The problem

"Is it a good beach day?" is harder to answer than it sounds. A sunny
forecast says nothing about a howling wind, cold water or a rough sea, and
the details that matter live in different places: a weather app for the sky,
a tide table for the water, a surf forecast for the waves. Surf forecast
sites are the closest thing to one view, but they're built for experienced
surfers, with dense tables of numbers and one beach at a time.

## Who it's for

- **Anyone heading to the beach:** families, swimmers, walkers, and visitors
  who don't know the local coast, checking whether it's worth the trip and
  which beach is best today.
- **Surfers,** especially beginners, who want to know when to go without
  reading a swell chart.
- **Surf schools and beach businesses** that want to show their customers
  the conditions. It's built to be leased as a branded conditions page.

## How it solves it

- **Live conditions for 34 beaches** in Cape Town, the greater Durban coast
  and the Eastern Cape, filterable by province: air and water temperature,
  wind and gusts, cloud and rain, waves, tide, and sunrise and sunset.
- **Compare beaches at a glance.** If one beach is windy or rough, you can
  see which nearby beach is calmer.
- **Best times to surf.** It picks the best two-hour surf windows today and
  tomorrow, and the best beach for surfing right now, so nobody has to
  interpret the data.
- **A three-day forecast** chart per beach.
- **Conditions you can see.** Each beach has its own scene, and the sky, sea
  and stick figures on the sand change with the live weather, so a glance
  tells you more than a table would.
- **Built to scale cheaply.** On the live site, a serverless function fetches
  every beach in two API calls and the CDN caches the result for 20 minutes,
  so API usage stays flat however many visitors arrive, and the API key never
  reaches the browser.

## Tech stack

- Vanilla HTML, CSS and JavaScript (ES modules, no framework)
- [Open-Meteo](https://open-meteo.com/) marine and weather APIs
- Netlify Functions for the cached conditions endpoint
-- Built on an earlier single-beach concept, scaled up to 34 beaches

## Status

Working concept, live on the CornerStone TechDev site and being pitched to
surf schools. Next up: a general "beach day" rating alongside the surf
score, so non-surfers get a plain answer too. The production copy is
deployed from the
[cornerstone-techdev](https://github.com/KatlegoM18/cornerstone-techdev)
repo; this repo is the standalone version.

## Run it locally

Open the folder in VS Code and start **Live Server**. Locally the page calls
Open-Meteo's free API straight from the browser, which is fine for building
and demoing (non-commercial). If the feed can't be reached it falls back to
clearly labelled sample data.

Try `?beach=supertubes`, `?beach=umhlanga`, `?beach=coffee-bay` and so on, or
pick a beach from the dropdown or the grid.

## Deploy

Deployed on Netlify, the page reads `/api/paddle-out/conditions`, served by
`netlify/functions/paddle-out-conditions.mjs`. Set `OPEN_METEO_KEY` in
Netlify's environment variables once a commercial Open-Meteo plan is active;
without it the function uses the free API.

## Adding or tuning beaches

Everything beach-specific is in `js/beaches.js`:

- `lat` / `lon`: a point just off the beach
- `offshore`: the bearing the wind blows **from** when it's offshore
  (first-pass values; tune with local surfers)
- `EXPOSURE`: how much of the open-ocean swell reaches the beach (the
  forecast grid is about 8 km wide, so neighbouring beaches share a forecast
  point)

Landmarks are in `js/landmarks.js`; the beach-life animation is in
`js/life.js`.

---

Built by [Katlego Mokgofa](https://github.com/KatlegoM18) /
[CornerStone TechDev](https://cornerstonetechdev.co.za).
