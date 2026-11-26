# ArtVision Today — Search Bar Integration

The ArtVision opportunity index uses `public.opportunities` in Supabase.

## Already deployed
- Database: `xtkdnyqjheewsqnvugaj`
- Search RPC: `public.search_artvision_opportunities`
- Public read-only API:
  `https://xtkdnyqjheewsqnvugaj.supabase.co/functions/v1/artvision-opportunity-search`
- Source updater:
  `DrkSiddh/N3W-M0N3Y-Automation/.github/workflows/sync-opportunities.yml`
- Search enhancement: `artvision-opportunity-search.js` in this repository.

## Netlify integration (site: artvision-today.netlify.app / artvision.today)

The existing site has search input `#drop-search` and results container `#drop-list`.
Netlify can inject one script without changing the site's source:

1. Open the **artvision-today** site in Netlify.
2. Go to **Project configuration → Developer settings → Post processing → Snippet Injection**.
3. Add a new snippet named `ArtVision Opportunity Search` positioned **before </body>**.
4. Paste:

```html
<script src="https://cdn.jsdelivr.net/gh/DrkSiddh/ArtVision-Opportunities-Database@main/artvision-opportunity-search.js" defer></script>
```

5. Save; verify at `https://artvision.today/#drop`. Netlify's snippet injection applies at request time.

## Expected test cases
- **OMI**: Art Omi historical listing, marked with a past deadline.
- **New York painters**: match relevant NYC visual-artist opportunities.
- **December 1**: return opportunities with the 2026-12-01 deadline.
- **Bernheim**: return Bernheim Forest, with upcoming November 30, 2026 deadline.
- Empty input: show upcoming opportunities (historical applications are hidden by default).

Every result includes the URL, deadline, award/support details and eligibility when available.
Historical entries must be labeled as past-deadline entries, not presented as open.

The script is a progressive enhancement specifically for the existing `#drop-search` and `#drop-list`; it does **not** require ElevenLabs or an LLM.
