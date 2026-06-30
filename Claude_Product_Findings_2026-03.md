# Claude Product Findings: A Reproducible Code-Block Encoding Bug and Three UX Observations

*Findings identified during a multi-hour build session (Claude Sonnet 4.6, March 20, 2026) and submitted to Anthropic through the in-product feedback interface. The session involved a first-time, non-technical user standing up a Python environment from scratch and running a live data pipeline with Claude's help. The findings below are reproducible and are ordered by likely engineering impact.*

---

## Finding 1 — Reproducible bug: non-ASCII characters in rendered code blocks

**Summary.** The claude.ai browser interface renders certain code-block content using Unicode punctuation, specifically the em dash (U+2014) and smart quotes (U+2018 / U+2019), in place of ASCII hyphens and straight quotes. When that code is copied from the browser and pasted into a Python editor, Python raises `SyntaxError: invalid character`.

**Reproduction.**
1. Ask Claude to write a Python script that includes comments and string literals.
2. Copy the rendered code from the claude.ai browser interface.
3. Paste it into IDLE or VS Code and run it.
4. Observe a `SyntaxError` on the line containing the substituted character.

**Affected editors confirmed.** IDLE, VS Code.

**Why it matters.** This disproportionately affects non-technical users, who are the most likely to reach for IDLE as a first editor and the least likely to recognize a Unicode-substitution error for what it is. The code looks correct on screen, so the failure gives no visual cue to its cause.

**Suggested fix.** Render code blocks in plain ASCII, or normalize/strip non-ASCII punctuation within code blocks before display.

**Workaround adopted in-session.** Every script generated for the remainder of the session carried an explicit instruction to use ASCII-only characters throughout, with no em dashes, smart quotes, or other Unicode punctuation. This removed the error entirely and was later baked into the project's standing prompt.

---

## Finding 2 — Obstacles were resolved reactively rather than proactively

During environment setup, each obstacle was resolved efficiently, but only after the user encountered it and reported it. Three examples from a single session: the system `PATH` did not include Python or pip; a Microsoft Store Python stub shadowed the real interpreter and returned a misleading version string; and IDLE silently auto-converted straight quotes into curly quotes, causing typed code to fail.

For a non-technical user on an implementation task, anticipating the next two or three likely obstacles before they are hit is materially more valuable than troubleshooting after the fact. A lightweight "here is what will probably go wrong next, and how to handle it" step at the start of an implementation task would have compressed the session noticeably and reduced the number of dead ends the user had to walk into first.

---

## Finding 3 — Long-session collaboration showed a different quality distribution than single-turn use

Output quality compounded across the session in a way that was qualitatively different from single-turn interactions. The final design was substantially different from the initial one, and the most significant improvements were driven by user questions the model had not anticipated. This suggests that sustained collaborative work may be worth treating as a distinct interaction mode with its own quality characteristics, rather than as a sequence of independent turns, and may be worth studying as such.

---

## Finding 4 — Practical constraints were elicited late

Responses optimized for theoretical completeness before practical deployability. Exchange recommendations assumed access to trading venues that were unavailable under the user's state regulations, until that constraint was surfaced by a user question; architecture recommendations assumed a Linux or cloud deployment target before the user's actual Windows home machine was surfaced. A short up-front elicitation of operating system, technical background, and regulatory jurisdiction would have improved early-response quality on an implementation task, before the first script was ever run.

---

## Note

All four observations were submitted to Anthropic as constructive product signal. Finding 1 is a concrete, reproducible defect with a clear fix; Findings 2 through 4 are interaction-design observations from the specific vantage point of a first-time, non-technical user, the population least equipped to diagnose these issues on their own and therefore the most useful lens for surfacing them.
