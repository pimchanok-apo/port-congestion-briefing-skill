# Port Congestion Briefing — Claude Skill

**Category:** Skill
**Author:** Pimchanok A.

## What it does

`port-congestion-briefing` teaches Claude to research current port
congestion, vessel ETA delays, berth waiting times, and disruption risk
(strikes, weather, customs backlogs, equipment shortages) for a named port
or trade lane, then turn that research into a short, dated, sourced briefing
that a shipping/logistics operations team can act on immediately.

Example prompts it triggers on:
- "What's the situation at Laem Chabang right now?"
- "Any delays expected for our Shanghai booking this week?"
- "Give me a port congestion briefing for the Bangkok–Rotterdam lane."

## Why a Skill, and not an MCP server, Plugin, or CLI tool

This came out of comparing the four product types directly against what the
task actually needs:

- **Skill fits because the hard part is judgment, not access.** There's no
  single authoritative live-data API for global port congestion — the real
  work is knowing *which* sources to check for a given region, weighing
  conflicting reports, and writing the result in a consistently scannable
  format. A Skill — "repeatable instructions and resources," per the course's
  *What Makes a Great ChatGPT App* reading — is exactly the right shape for
  that: it packages judgment and a template, and reuses whatever search/browse
  capability the host already has, instead of standing up new infrastructure
  for it.
- **An MCP server** would make sense if this were wrapping one reliable,
  structured, live data source (e.g. a single paid congestion-tracker API)
  — the *Brainstorm Plugin Use Cases* reading calls that out as the
  "Know"/live-data case for MCP servers specifically. That's a natural
  next step if RCL later gets access to something like project44 or
  Linerlytica with an API — see Limitations below.
- **A Plugin (ChatGPT app)** was a mismatch because this task doesn't need a
  visual UI — no card, carousel, or fullscreen view adds anything over a
  well-formatted text briefing (the *UI Guidelines* reading's whole point is
  that visual UI should only appear when it earns its place, and a status
  report read once doesn't need one).
- **A CLI tool** was a mismatch because the task is research-and-judgment,
  not a deterministic transform — there's no fixed input file to run a
  script against.

## How it works

1. Pin down which port(s)/lane and timeframe are in scope.
2. Search multiple source types (port authority notices, carrier advisories,
   trade press, optionally paid trackers) rather than one generic query —
   see `port-congestion-briefing/references/sources.md` for a region-by-region
   list of what to check and what each source is actually good for.
3. Extract congestion level/trend, berth wait vs. baseline, and any named
   disruptions with dates, for each port.
4. Write the result into a fixed template (Summary → Port-by-port status →
   Watch items → Recommended action), always dated and sourced, and flags
   explicitly when good data wasn't available rather than guessing.

A fully worked (illustrative, clearly labeled fictional) example is in
`port-congestion-briefing/references/example-briefing.md`.

## Files in this submission

```
port-congestion-briefing/
├── SKILL.md                        — triggering description + full workflow
└── references/
    ├── sources.md                  — where to look, by region
    └── example-briefing.md         — worked example of the output format
port-congestion-briefing.skill      — packaged/installable version (zip)
README.md                           — this file
```

## Try it

- **Claude.ai / Cowork:** upload `port-congestion-briefing.skill` — it shows
  a "Save skill" option that installs it directly.
- **Claude Code / local:** unzip `port-congestion-briefing.skill` (or copy
  the `port-congestion-briefing/` folder) into your skills directory.
- Then ask something like *"What's the port congestion situation at Laem
  Chabang this week?"* and Claude should pick the skill up automatically.

## Limitations & next step

This skill depends entirely on whatever web search/browsing the host Claude
has — it was drafted and validated for structure in an environment where
live web search was disabled, so it hasn't been run end-to-end yet. It's
worth a live test run in a search-enabled environment (Claude.ai or Claude
Code) before relying on it operationally.

If RCL later has API access to a paid congestion tracker (project44,
Linerlytica, MarineTraffic Pro, etc.), the natural evolution is to promote
the "live data" part of this into a small MCP server that this skill (or
any other tool) can call for a authoritative number, while keeping the Skill
for the judgment/formatting layer on top.
