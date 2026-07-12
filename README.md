# Second Home OKF Bundle

An [Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md) v0.1 knowledge bundle for **Second Home**, a cafe/bar/event space in Fushimi, Nagoya. It's meant to give a customer-facing AI agent grounded, up-to-date context about the venue: hours, menu, and events.

## What's in here

```
bundle/
├── index.md      # entry point — links into the sections below
├── about.md      # venue info: location, hours, history, social media, event organizers
├── cafe/         # Second Home's daytime cafe: menu items (sourced from customer reviews — no official menu yet)
└── events/       # Second Home's nighttime side: Global Friends' events (+ other organizers)
```

Every concept file (everything except `index.md`) is a plain markdown file with a small YAML frontmatter block (`type`, `title`, `description`, ...) and a markdown body. No tooling or build step is required — it's meant to be readable as-is by both humans and agents.

Second Home is mainly two things: a **cafe by day** and **Global Friends in Nagoya's events by night** (plus a few other organizers) — hence the parallel `cafe/` and `events/` directories. Shared facts that apply to the whole venue (location, ownership, payment, etc.) live in `about.md`.

## Key things to know

- **Second Home's events are run by [Global Friends in Nagoya](https://www.meetup.com/global-friends/)**, the community that originally rented the space before it had a bar or cafe. The cafe is a separate business under the same ownership. See `about.md` for the full story.
- **The cafe menu isn't official** — Second Home hasn't published one, so the items here are reconstructed from Tabelog reviews and should be treated as illustrative. The evening bar menu isn't documented yet.
- **Event dates and theme names are illustrative, not a live schedule.** Check [Global Friends on Meetup](https://www.meetup.com/global-friends/events/) for what's actually on.

## Sources

Content is compiled from [Second Home's Tabelog page](https://tabelog.com/en/aichi/A2301/A230102/23094880/), the Global Friends and Cosmo International Party Nagoya Meetup pages, and facts provided directly by the venue operator. Each concept file cites its sources.
