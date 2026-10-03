# Developer Experience Dashboard (mockup)

Clickable prototype of the Altimetrik Developer Experience dashboard for AI coding tool limits (Cursor, GitHub Copilot, Claude).

## Run

Open `index.html` in any browser. No build step and no install. Needs internet only for the icon font.

To serve it locally instead:

```
npx serve .
# or
python3 -m http.server 8080
```

## What's in it

**Developer view**
- Overall tab with combined spend across tools, plus a tab per tool
- Monthly limit, usage, remaining budget, and cost breakdown per tool
- Quick nudge: one-tap, auto-approved limit increase. Unlocks only when usage is at or above the threshold (default 95%) or remaining budget is below the nudge amount
- Custom request for larger increases, with manager approval
- Request history

**Admin view**
- Analytics: requests today, dollars added, pending approvals, active requesters, 7-day trend, today by tool, top requesters
- Approvals: approve or reject custom requests, with flags for "Above tool max", "Over combined cap", "Already reached"
- Settings
  - Overall: master switch for quick nudges, max nudges per user per month across tools, optional combined cap across tools
  - Per tool (Cursor, Copilot, Claude): visible to developers, base monthly limit, quick nudges on/off, custom requests on/off, nudge amount, max nudges per day, max nudges per month, unlock threshold, max request limit, and a live "max a user can be provisioned" preview

## Nudge rules

A nudge is allowed only when all of these pass:

1. Quick nudges are on globally and for the tool
2. Usage >= threshold, or remaining < nudge amount
3. Daily count for the tool is under the limit
4. Monthly count for the tool is under the limit
5. Monthly count across all tools is under the overall limit
6. If the combined cap is on, the new total stays under it

## Notes

- All data is sample data held in memory. Refreshing resets it.
- Defaults live in the `config` object at the top of the script.
- Daily and monthly resets should use the org time zone in the real backend.
