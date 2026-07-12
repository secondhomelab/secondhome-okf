# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This repo holds an **OKF (Open Knowledge Format) v0.1 bundle** for Second Home, a cafe/bar/event space in Nagoya, Japan. It is not a software project — there is no build, lint, or test tooling. The deliverable is the markdown content itself, meant to be consumed by a **customer-facing AI agent**.

The full OKF v0.1 spec: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md

## Bundle structure

All content lives under `bundle/`. Every `.md` file except `index.md` and `log.md` is a **concept document** and MUST have a YAML frontmatter block with a non-empty `type` field (e.g. `Venue`, `Menu Item`, `Event`). `index.md` files have no frontmatter except the bundle-root `bundle/index.md`, which carries `okf_version: "0.1"`.

```
bundle/
├── index.md          # bundle root, okf_version frontmatter, links into the sections below
├── about.md           # type: Venue — venue-wide facts shared across cafe/bar/events (location, ownership, payment, ...)
├── cafe/               # type: Menu Item concepts — Second Home's daytime cafe (no official published menu, no bar menu documented yet)
└── events/             # type: Event concepts — Second Home's nighttime side, mostly Global Friends in Nagoya
```

`cafe/` and `events/` are deliberately parallel: Second Home is, in practice, two things — a cafe by day and Global Friends in Nagoya's events by night (plus a couple of other organizers). Venue-wide facts that apply to both (and to the bar) stay in `about.md` rather than being duplicated into either directory.

Conformance check (every concept has a `type` field):
```bash
for f in $(find bundle -name "*.md" ! -name "index.md"); do grep -q "^type:" "$f" || echo "MISSING type: $f"; done
```

## Content conventions established in this bundle

- **No `log.md`.** OKF allows an optional update-history log, but this bundle intentionally omits it — the content is for a customer-facing agent, not an internal audit trail. Don't reintroduce it.
- **`about.md` is the canonical source of truth** for facts referenced elsewhere (org relationships, membership stats, hours). Other files should *link* to the relevant `about.md` section (e.g. `/about.md#global-friends-in-nagoya`) rather than restating the fact. This was a deliberate cleanup — earlier drafts repeated the same sentences across 5+ files; avoid reintroducing that.
- **Cross-links use bundle-absolute paths** (`/about.md`, `/events/international-party.md`), the form the spec recommends since it's stable when files move within their subdirectory.
- **`cafe/` covers the cafe only.** Its items are sourced from Tabelog customer reviews, not an official published menu (Tabelog itself has no menu photos as of writing) — treat as provisional/best-effort, not confirmed pricing/availability. The bar's menu isn't documented anywhere in this bundle yet.
- **Event dates and theme names are illustrative, not a live schedule.** Global Friends in Nagoya's recurring weekly/monthly slots (Saturday, Wednesday, Friday, monthly Quiz Night, monthly DJ Freestyle) rotate through different named theme nights (e.g. the Saturday slot might run as "International Party" one week and "Burger Party" the next). Any specific dates recorded here were pulled from Meetup/RSS at a point in time and will go stale — event files link to https://www.meetup.com/global-friends/events/ for the live schedule, and this pattern should be preserved/extended for any new event content.

## Key real-world relationships (don't re-derive from scratch — read `about.md`)

- **Global Friends in Nagoya** is the community that originally rented the space and, for practical purposes, *is* Second Home's events program (Saturday International Party, Wednesday Midweek Mixer, Friday Night Meetup, monthly Quiz Night, monthly DJ Freestyle).
- **The cafe operates independently of Global Friends** — same owners, separate business. The venue's history is: events-only space (Global Friends) → added bar → added cafe (Tabelog lists the cafe's start date as 2026-02-28, which is *not* the venue's founding date).
- **Cosmo International Party Nagoya** and **Aichi Connection** are external/independent communities that also host events at Second Home — distinct from Global Friends, listed under "Other Event Organizers" in `about.md` and "Externally-organized events" in `events/index.md`.

## Sourcing

Primary sources used so far: the venue's Tabelog page, the Global Friends and Cosmo Meetup pages (and Global Friends' RSVP RSS feed), and facts provided directly by the venue operator in conversation (flagged as such in each file's Citations section). Instagram and Facebook pages are not fetchable via WebFetch (JS-rendered) — only their URLs/handles could be recorded, not bio content.
