# Agent Kairova

A four-agent job search system built on Claude AI.

Most job search tools help you apply faster. Agent Kairova helps you apply smarter — surfacing the right roles before they're picked over, turning your publishing into an inbound pipeline, and getting sharper about what's actually working over time.

[**Live Demo →**](https://iancowpar.netlify.app/)

---

## What It Does

Agent Kairova runs four agents on a configurable schedule:

**Agent 01 — Daily Search**
Searches 17+ job sources before LinkedIn indexes them. Runs a live-check gate on every URL so stale listings never reach you. Scores each role against your profile — comp floor, geography, mission alignment, connection path — and ranks by tier. Drafts cover letters for Tier 1 roles in your voice. Delivers a daily briefing with one highest-leverage move.

**Agent 02 — Content Engagement**
Monitors Substack and LinkedIn engagement twice a week. Cross-references every engager against your target companies and your connection graph. Turns publishing activity into a warm inbound pipeline — not just brand-building.

**Agent 03 — Interview Intelligence**
Fires the night before each interview. Researches the company's live operational reality, builds an interviewer profile from published work, and surfaces the real problem underneath the job description. Delivers a full prep brief: opening statement, sharp questions, competitive landscape.

**Agent 04 — Feedback Loop**
Tracks every outcome. Calculates response rates by connection path, source category, cover letter angle, and mission type. Recalibrates Tier 1/2 scoring as data accumulates. The system gets sharper the longer you use it.

---

## Architecture

```
profile.json          # Who you are — swappable per user
tracker.json          # Live state — roles, outreach, interviews, outcomes
master-resume.json    # Structured resume data with tagged bullets for tailoring
agent prompts         # Generic system logic — reads from profile, writes to tracker
```

The profile layer is fully separated from the system logic. User #2 swaps in their own `profile.json` and the agents work without modification.

**Resume tailoring** is built into the apply flow. Every role gets a tailored resume: the summary is rewritten for the JD, skills are reordered to match JD language, and experience bullets are ranked by relevance score. Outputs both an HTML (print to PDF) and a plain-text ATS version.

**Live-check gate** runs on every surfaced role before it enters the tracker. Stale listings are dropped silently — they never reach the user.

**Performance patterns** recalibrate automatically at 5+ data points per dimension (connection path, source, cover letter angle, mission type). The scoring model improves with use.

---

## Stack

- **Runtime:** Claude AI (Anthropic) via Claude Code CLI
- **Scheduling:** Cron-based scheduled tasks — weekdays 10am, Tue/Fri 9am, plus event-triggered (interview night-before)
- **State:** JSON flat files (`tracker.json`, `profile.json`, `master-resume.json`)
- **Sources:** Greenhouse direct endpoints, Lever direct endpoints, PM-specific boards, startup boards, broad boards
- **Delivery:** Email + local file output

No database. No backend. No framework. The agents read files, write files, and call the Claude API.

---

## Demo

The live demo shows all four agents running their tasks in real time — terminal output, then deliverable. Built for voiceover walkthroughs and investor/partner pitches.

Controls: **Space** to pause/resume · Speed selector (1×/2×/4×) · Skip to deliverable

Dashboard includes: live pipeline metrics, comp target slider, thumbs up/down feedback on recommendations (trains the scoring model), and agent learning progress tracker.

---

## Status

Active and running in personal use. Productization in progress.

If you're a job seeker, career coach, or recruiting platform interested in what this looks like as a real product — [reach out](mailto:ian.cowpar@gmail.com).

---

*Built by [Ian Cowpar](https://linkedin.com/in/ian-cowpar) · [The Unofficial Leader](https://theunofficialleader.substack.com)*

