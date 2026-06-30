# ai-portfolio
 
AI evaluation, structured prompting, and applied research by a risk and compliance professional who treats AI as infrastructure, not as a search engine.
 
## About
 
Since March 2026 I have used AI as a primary thinking and production tool across compliance systems design, legal and financial research, business analysis, software scaffolding, and AI evaluation, with no formal technical background. Rather than treating models as authoritative, I use them as collaborators whose outputs are tested, verified, and refined through human judgment. This repository collects the work that holds up as evidence of what that approach produces.
 
I am a risk and compliance operations professional by background. The thread running through everything here is the same one that runs through my day job: find what a system gets wrong, trace it to its root, and design the process that catches it the next time.
 
## Start here
 
If you read one item, read **[RCA-001](ai-evaluation/RCA-001.md)** — a root-cause analysis of a documented Claude failure mode, written the way a safety or evaluation team would document one internally. It is the clearest single example of how I work.
 
## What's here
 
*Each folder below is a standing category. Listed under each is what it holds today. The repository is added to over time, so categories grow and new ones appear as work is finished and cleared for publication.*
 
### `ai-evaluation/` — structured analyses of model failures and product issues
 
**RCA-001 — Claude character-counting failure.** A structured root-cause analysis of a documented model failure mode: a tokenization-driven miscount that compounded into overconfidence and terminological entrenchment. Written in the format an evaluation or safety team would use internally, with an incident timeline, layered failure-mode analysis, impact assessment, detection analysis, and recommendations for both users and developers.
 
**Claude product findings — code-block encoding bug and UX observations.** A reproducible defect (the browser interface injecting non-ASCII punctuation into code blocks, which then breaks on paste into a Python editor) together with three interaction-design findings, identified during a live build session and submitted to Anthropic through the in-product feedback interface. Written from the vantage of a first-time user, the population least equipped to diagnose these issues and therefore the most useful lens for surfacing them.
 
### `prompt-engineering/` — self-designed prompt architectures for structured work
 
**Crypto token research engine.** A master prompt that turns a general-purpose model into a standardized, institutional-grade research engine: name a token, and it runs an eight-stage pipeline into a fixed 16-section report. The discipline is the point. Every factual claim is tagged against a five-tier source-reliability system; training knowledge is explicitly barred as a substitute for live research; a mandatory self-critique stage requires the model to list at least ten of the analysis's own weaknesses before it proceeds; and separate numerical-verification, consistency-audit, and precision-calibration passes run before anything is finalized, with a Source Audit Table and a Verification Gaps appendix flagging what could not be confirmed. It forces distinctions most analysis blurs, such as value accrual to the company versus the protocol versus the token itself, and it requires stating in advance the conditions that would prove each thesis wrong. Run across roughly 28 tokens in a four-day stretch; the methodology held at volume.
 
### `research/` — applied quantitative and domain research
 
**BTC→altcoin lag study.** A self-directed quantitative research project: a stated hypothesis that liquid altcoins lag Bitcoin's price moves, tested against roughly 80 million ticks of historical data through a pipeline built from scratch, under a strict test-to-find-out discipline. Documents the methodology, the findings (including dropping the original target asset once the data ranked it lower), and an honest current status: supported in historical data, not yet validated live. A demonstration of rigor and of being willing to let evidence override the starting assumption.
 
## Evaluation philosophy
 
Across these projects the approach is consistent:
 
- verify rather than assume
- investigate anomalies instead of dismissing them
- distinguish confidence from evidence
- document uncertainty rather than hide it
- preserve human judgment where mistakes carry real cost
## How this was made
 
Everything here was produced in collaboration with AI, mostly Claude, by someone who cannot write the underlying code unassisted. That is the point. The work reflects a consistent method: use the model to move fast, then apply judgment at every step where being wrong would carry a cost, verify outputs rather than trusting them, and document the failures as carefully as the successes.
 
---
 
*This repository is added to as new work is produced and cleared for publication.*
 
