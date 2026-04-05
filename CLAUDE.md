# Ireland Family Trip — Travel Planner Website

## What this is
A single-page travel itinerary website (`index.html`) for an 8-day Ireland family trip (6–13 April 2026). Built as a self-contained HTML file with inline CSS and JavaScript. Deployed via GitHub Pages.

## Live site
https://iamreallynotamy.github.io/cautious-broccoli/

## Source of truth
- **Website**: `index.html` in this repo — the primary artifact, always kept up to date
- **Detailed markdown**: `Z:\My Drive\Trip 20260406 Ireland\trip-plan.md` — comprehensive reference doc (may be slightly behind the website after recent changes)
- **Booking PDFs**: `Z:\My Drive\Trip 20260406 Ireland\*.pdf` — named in format `date - hotel/travel - name.pdf`

## Key architecture decisions
- **Single HTML file** — no build tools, no framework, works offline (except weather API)
- **Leaflet.js + CartoDB Voyager tiles** for maps (free, no API key)
- **Open-Meteo API** for weather forecasts (free, no API key)
- **i18n**: Chinese (zh) is default language, English (en) available via toggle. All visible text uses a `t()` translation function with `translations.en` and `translations.zh` objects
- **Day tabs**: 8 days, one active at a time. Each day has: header, map, itinerary timeline, activities, hotel card, weather forecast, documents list
- **Split day support**: Day 4 (Thu) uses `isSplitDay: true` with `segmentsGroupA` (S) and `segmentsGroupB` (Rest of family), plus a shared morning `segments` array rendered before the split

## Trip overview
- **Travellers**: 4 adults + 2 children (Lily 5yo, Ruyi 3yo)
- **S** flies home Thu 9 Apr from Belfast; rest of family continues to Dublin/Cork/Cobh
- **Route**: London → Belfast → Derry → North Coast → Belfast → Dublin → Cork → Blarney → Cobh → London

## Current status
- **Mon 6 – Thu 9 (Days 1–4)**: Fully planned with detailed itinerary, restaurants, attractions, maps
- **Fri 10 – Mon 13 (Days 5–8)**: Have detailed itineraries from AI suggestions integrated, but user wants to **revise these days further**. Treat them as drafts.

## Naming conventions
- "S" = Sijia (in both EN and ZH)
- "Rest of family" (EN) / "其余家人" (ZH) = Mark + grandparents + 2 kids
- "M" = Mark

## Hotels (current)
| Night | Hotel | Notes |
|-------|-------|-------|
| Mon 6 | voco Belfast | Gasworks, BT7 2JB |
| Tue 7 | Holiday Inn Express Derry | 1 night only |
| Wed 8 | Leonardo Hotel Belfast | No on-site parking → Great Northern Carpark £12/24h |
| Thu 9–Fri 10 | Clayton Hotel Charlemont Dublin | Family only |
| Sat 11–Sun 12 | Moxy Cork | Prepaid €554 non-refundable |

## Key things to remember
- Tuesday/Wednesday were swapped (bad weather on north coast Tuesday → do Derry city Tuesday, scenic drive Wednesday)
- Monday is Easter Monday — prioritise free attractions
- Titanic Belfast: exterior only (free), added to Thursday morning
- Belfast City Hall: moved to Wednesday afternoon (right next to Leonardo Hotel)
- Cork City Gaol: on Sunday (on the way back from Blarney, NW→W→Centre route)
- Monday Cork: English Market for breakfast + Farmgate Café brunch, then Cobh, then airport. No backtracking (Centre→E→S sweep)
- Dublin-Cork hire car: **still not booked, no PDF**
- Book of Kells at Trinity College: **requires advance booking**

## Data structure
Each day in the `days` array has:
```
{
  date, weekday, title: {en, zh}, location: {en, zh},
  travelers, weatherKey, isSplitDay?,
  segments: [{type, icon, title:{en,zh}, time, duration, mapUrl?}],
  segmentsGroupA?, segmentsGroupB?,
  activities: {en: [], zh: []},
  hotel: {name, addr, rooms, checkin, checkout, note?, mapUrl},
  pdfs: []
}
```

Map locations are in a separate `dayLocations` array indexed by day.

## Workflow
- Edit `index.html` directly in `D:\GitHub\cautious-broccoli`
- Commit and push to deploy to GitHub Pages
- The Google Drive folder has booking PDFs and the trip-plan.md reference doc
