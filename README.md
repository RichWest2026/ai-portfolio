# ai-portfolio
 
Work produced by a non-technical, self-taught user treating AI as infrastructure rather than as a search engine.
 
## About
 
Since March 2026 I have used AI as a primary thinking and production tool across compliance systems design, legal and financial research, business analysis, software scaffolding, and AI evaluation, with no technical background and no formal training. This repository collects the work that holds up as evidence of what a motivated, critical, non-technical user can build when they treat these tools as infrastructure and keep a human in the loop where it matters.
 
I am a risk and compliance operations professional by background. The thread running through everything here is the same one that runs through my day job: find what a system gets wrong, trace it to its root, and design the process that catches it the next time.
 
## What's here
 
*Each folder below is a standing category. Listed under each is what it holds today. The repository is added to over time, so categories grow and new ones appear as work is finished and cleared for publication.*
 
### `ai-evaluation/` — structured analyses of model failures and product issues
 
**RCA-001 — Claude character-counting failure.** A structured root-cause analysis of a documented model failure mode: a tokenization-driven miscount that compounded into overconfidence and terminological entrenchment. Written in the format an evaluation or safety team would use internally, with an incident timeline, layered failure-mode analysis, impact assessment, detection analysis, and recommendations for both users and developers. This is the piece I would point to first.
 
**Claude product findings — code-block encoding bug and UX observations.** A reproducible defect (the browser interface injecting non-ASCII punctuation into code blocks, which then breaks on paste into a Python editor) together with three interaction-design findings, identified during a live build session and submitted to Anthropic through the in-product feedback interface. Written from the vantage of a first-time, non-technical user, the population least equipped to diagnose these issues and therefore the most useful lens for surfacing them.
 
### `prompt-engineering/` — self-designed prompt architectures for structured work
 
**Vault Digital risk-analysis framework.** An eight-phase, self-designed prompt architecture for structured business-risk analysis, with forced iteration passes and explicit anti-hallucination checks. Applied to a real business question, it produced 97 risks across 13 categories and a calibrated go/no-go. Includes the prompt, the full analysis output, and a separate self-audit that evaluates the AI's own output for compression and research-quality gaps. The self-audit is the unusual part; most people never check their AI's work this way.
 
### `research/` — applied quantitative and domain research
 
**BTC→altcoin lag study.** A self-directed quantitative research project: a stated hypothesis that liquid altcoins lag Bitcoin's price moves, tested against roughly 80 million ticks of historical data through a pipeline built from scratch, under a strict test-to-find-out discipline. Documents the methodology, the findings (including dropping the original target asset once the data ranked it lower), and an honest current status: supported in historical data, not yet validated live. A demonstration of rigor and of being willing to let evidence override the starting assumption.
 
### `automation/` — working scripts and deployments
 
**Inventory alert system (Google Apps Script).** A working, deployed script that categorizes inventory by age and sends formatted daily email alerts. Directed, configured, and deployed by a non-technical user.
 
## How this was made
 
Everything here was produced in collaboration with AI, mostly Claude, by someone who cannot write the underlying code unassisted. That is the point. The work reflects a consistent method: use the model to move fast, then apply judgment at every step where being wrong would carry a cost, verify outputs rather than trusting them, and document the failures as carefully as the successes.
 
---
 
*This repository is added to as new work is produced and cleared for publication.*
