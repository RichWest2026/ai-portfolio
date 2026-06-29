# ai-portfolio

Work produced by a non-technical, self-taught user treating AI as infrastructure rather than as a search engine.

## About

Since March 2026 I have used AI as a primary thinking and production tool across compliance systems design, legal and financial research, business analysis, software scaffolding, and AI evaluation, with no technical background and no formal training. This repository collects the work that holds up as evidence of what a motivated, critical, non-technical user can build when they treat these tools as infrastructure and keep a human in the loop where it matters.

I am a risk and compliance operations professional by background. The thread running through everything here is the same one that runs through my day job: find what a system gets wrong, trace it to its root, and design the process that catches it the next time.

## What's here

### `ai-evaluation/`
**RCA-001 — Claude character-counting failure.** A structured root-cause analysis of a documented model failure mode: a tokenization-driven miscount that compounded into overconfidence and terminological entrenchment. Written in the format an evaluation or safety team would use internally, with an incident timeline, layered failure-mode analysis, impact assessment, detection analysis, and recommendations for both users and developers. This is the piece I would point to first.

### `prompt-engineering/`
**Vault Digital risk-analysis framework.** An eight-phase, self-designed prompt architecture for structured business-risk analysis, with forced iteration passes and explicit anti-hallucination checks. Applied to a real business question, it produced 97 risks across 13 categories and a calibrated go/no-go. Includes the prompt, the full analysis output, and a separate self-audit that evaluates the AI's own output for compression and research-quality gaps. The self-audit is the unusual part; most people never check their AI's work this way.

### `automation/`
**Inventory alert system (Google Apps Script).** A working, deployed script that categorizes inventory by age and sends formatted daily email alerts. Directed, configured, and deployed by a non-technical user.

## Coming soon

- Multi-phase crypto research-engine prompt and sample reports
- Credit-fintech research series and synthesis
- Anonymized compliance-automation case study
- Regulatory statutory-research example

## How this was made

Everything here was produced in collaboration with AI, mostly Claude, by someone who cannot write the underlying code unassisted. That is the point. The work reflects a consistent method: use the model to move fast, then apply judgment at every step where being wrong would carry a cost, verify outputs rather than trusting them, and document the failures as carefully as the successes.
