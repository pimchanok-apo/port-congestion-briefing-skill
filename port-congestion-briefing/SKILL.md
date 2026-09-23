---
name: port-congestion-briefing
description: Research current port congestion, vessel ETA delays, berth waiting times, and disruption risk (strikes, weather, customs, equipment shortages) for one or more ports or a trade lane, then produce a structured briefing a shipping/logistics operations team can act on. Use this skill whenever the user asks about port congestion, vessel delays, berth availability, ETA changes, terminal disruptions, or wants a status update or briefing on a port, terminal, or route — even if they just name a port ("what's the situation at Laem Chabang right now") or ask indirectly about a booking or route ("will our Shanghai shipment be delayed"), without using the word "briefing" at all.
---

# Port Congestion Briefing

## Why this exists

Port congestion, berth waits, and disruption risk change fast and don't live
in any one place — carrier advisories, port authority notices, news, and
tracker sites all say something slightly different, and a stale number from
last week reads as confidently wrong. The point of this skill is to pull
those sources together into one dependable pass, and to hand back a briefing
that an operations person can scan in under a minute and still trust,
because every claim in it is dated and sourced.

## Workflow

1. **Pin down scope.** Identify the port(s) or trade lane in question. If the
   user names a booking, route, or vessel instead of a port, work out which
   port(s) that implies. If they don't give a timeframe, default to "current
   conditions, as of today" rather than a historical trend — that's almost
   always what's useful in the moment.

2. **Research from multiple angles, not one search.** A single query tends to
   surface only news headlines, which are usually about the worst disruption,
   not typical conditions. Look across:
   - Port authority notices and terminal operator advisories
   - Carrier advisories for that lane (Maersk, MSC, CMA CGM, ONE, Hapag-Lloyd,
     COSCO, etc. — whichever call at the port in question)
   - General news search for strikes, weather events, customs slowdowns, or
     equipment/chassis shortages at that port in the last 1-2 weeks
   - Congestion trackers or dashboards if the user has access to one (e.g.
     project44, Linerlytica, MarineTraffic) — ask if they have a subscription
     rather than assuming, since these are often paywalled
   - See `references/sources.md` for a fuller list of where to look, organized
     by region.

3. **Extract, per port, the things that actually change a decision:**
   - Congestion level and its direction (worsening / stable / improving)
   - Berth/anchorage waiting time, and how that compares to the recent
     baseline for that port (a number alone is meaningless without a baseline)
   - Named disruptions: strikes, weather, customs backlogs, equipment
     shortages — with dates
   - Anything specific to the user's stated trade lane or carrier

4. **Be explicit about gaps.** If reliable, recent data isn't available for a
   port, say so plainly in the briefing rather than filling the gap with a
   guess or an old number presented as current — a wrong "all clear" is worse
   than an honest "couldn't confirm."

5. **Write the briefing using the template below.** Keep it scannable: a
   logistics coordinator should get the headline in the first two lines.

## Output template

Use this exact structure:

```
# Port Congestion Briefing — [Port(s) / Lane] — [Date]

## Summary
[2-3 sentences: overall status, and the single most important thing to act on]

## Port-by-port status
### [Port name]
- Congestion: [level + trend]
- Berth/anchorage wait: [current] (baseline: [recent typical])
- Active disruptions: [named events with dates, or "none reported"]
- Source(s): [links, with dates checked]

[repeat per port]

## Watch items
- [Anything trending toward becoming a problem, even if not urgent yet]

## Recommended action
- [1-3 concrete suggestions: reroute, buffer time, expedite, hold, no action needed]
```

If a port has no usable data, keep its section but replace the bullets with
"No reliable recent data found — recommend checking [specific source] directly."

## Judgment calls

- **Don't inflate severity.** A single delayed vessel is not "severe
  congestion" — reserve strong language for when multiple independent
  sources agree conditions are actually bad.
- **Recency beats volume.** A short briefing built from three dated,
  corroborating sources beats a long one padded with old or single-sourced
  claims.
- **Always date-stamp the briefing and every source**, since the whole point
  of this document is that it can go stale within days.

See `references/example-briefing.md` for a fully worked example, and
`references/sources.md` for where to look by region and what each source is
actually good for.
