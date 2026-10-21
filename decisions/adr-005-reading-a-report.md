# Everyarc — ADR 005: Reading a school report, on the phone
*Decided by Hew, 2026-10-20. Supersedes the lines named under "What changes" in `everyarc-evidence-intake.md`, `everyarc-stack.md`, `everyarc-standards-and-safeguards.md`, `everyarc-build-spec.md` and `everyarc-bridge-contract.md`. Everything else in those docs, and every other doc, stands.*
*v0.1 · 2026-10-20 · Shared. Change it through this doc's changelog.*

---

## Decision
A parent can photograph a teacher's report (or choose a PDF, or paste its text), and Everyarc adjusts the child's plan from it, but only after the parent has seen three things and approved:
1. **What's left out.** The report is read **on the parent's phone**. Names, the school, IDs, emails, phone numbers and addresses are struck out there, and the parent confirms the text that will leave. The photo never leaves the phone.
2. **What Everyarc understood.** Each need or strength, with the report's own words, the skill it points to and how sure the reading is. The parent keeps, removes or re-points each one.
3. **What Everyarc will do.** Close the gaps first for a few weeks; lean into challenge where the report says the child is ready; keep fluency practice going everywhere else, as usual; and check each one with a few short items first, because what the child shows outweighs any report.

Nothing changes until the parent taps **Approve**. The change starts with the next day's path.

### How it works
- **On the phone:** OCR (tesseract.js, self-hosted) for photos and scanned pages, pdf.js for PDFs, or the parent's own pasted text (iPhone Live Text reads handwriting well). Redaction is deterministic: the household's own names (children, adults, contacts, the school and district), titles followed by a name, labeled fields, school-shaped names, contact details, long ID numbers, and likely names from public-domain name lists. The parent can strike any other word.
- **On the server:** the Edge Function `intake-read` checks the caller, the household's switch, and the text again for any known family name, and **refuses rather than trims** if one is left. Only then does it send the text to Anthropic (Sonnet 5.5, structured outputs, US inference, synchronous; no Batch or Files API).
- **The model only maps.** It returns quotes from the text, each mapped to a skill or topic with a direction and a confidence. Every quote must appear verbatim in the text sent; skills must be in the graph; any quote naming a condition is set aside, unused. **No sentence a parent reads is written by a model:** they see the report's own quotes and Everyarc's templated sentences, checked by the language validator.
- **What crosses to the learning side:** priors (skill-level, text-free, low weight, `confirm: true`) and plan targets. Two new plan levers make that matter (contract P17):
  - **`challenge`**, a target status: challenge skills come first among in-progress and new skills, the next skill after a fluent one comes sooner, stretch above grade is allowed there, and the block's harder item comes from there.
  - **`until`** on a target: a near-term priority or challenge that ends on a date.
  Neither ever gets around the fluency gate: a skill is core work only when what it rests on is fluent, and a priority whose basics aren't solid steps back to them first.
- **Confirming checks** run at any time, not only during discovery: a prior on a skill the child hasn't shown yet gets two short items in warm-up, and the skill's state says whether the report was borne out.

### Scope of v1
Report cards, progress reports, teacher notes and emails, test score reports and worksheets. **IEPs, 504 plans and evaluations aren't read in v1**: they're recognized on the phone and nothing is sent. The mail drop, curricula and dictation stay in the second wave.

### Who uses it first
Hew's household, behind a switch only the operator can set, on Anthropic's standard API terms (no training on API data). Only redacted text is sent. Every other family waits for zero data retention, counsel (LAW-22) and the redone impact assessment (R-08).

## Why
- The parent sees and confirms what leaves before it leaves; that's stronger than a server-side redactor the parent never sees, and nothing Python runs in production.
- A model that only maps quotes to skills can't put words in a teacher's mouth, can't name a condition, and can't be talked into acting by the document: it has no tools and nothing it returns takes effect without the parent.
- Priors that only mattered in a child's first twelve tries couldn't carry a report's weight. A challenge lever and a time-boxed priority do, without bending the fluency gate.

## What changes
| Doc | Line | Now |
|---|---|---|
| `everyarc-evidence-intake.md` | Gate 1 channels; Presidio; on-device Vision OCR | Photo, PDF and paste on the web; reading and redaction on the phone, confirmed by the parent; IEPs, 504s and evaluations not read in v1 |
| `everyarc-stack.md` | Rows 76–88 (VisionKit, Vision OCR, Presidio, page images to the model) | tesseract.js and pdf.js on the phone; text only to Anthropic |
| `everyarc-standards-and-safeguards.md` | STD-04's mechanism (Presidio) | On-device recognizers plus parent confirmation, re-checked on the server; the test is unchanged: zero identifiers reach the extraction prompt |
| `everyarc-build-spec.md` | M5 pipeline step 2–3 (images to the model; Haiku for common sources) | Text only; Sonnet 5.5 for v1 |
| `everyarc-bridge-contract.md` | §5 plan targets | P17: `challenge` status and `until` on a target |

## What doesn't change
Intake is optional and never a gate (D08). Filing isn't using: nothing a report says shapes the plan until the parent accepts it. Priors cross text-free; nothing from a report reaches the iPad. Originals aren't kept (here, they never leave the phone). The fluency gate.

## Not claimed
That a report's reading is right: the parent reviews it, and the child's own work outweighs it. That Everyarc understands a child's needs beyond the skills it can practice.

## Revisit when
The golden-set eval misses its thresholds on a document type; ZDR and counsel land (widen beyond Hew's household); a literacy graph exists (reading claims stop being notes); the mail drop arrives.

## Changelog
- v0.1 · 2026-10-20 · Hew's decisions: read on the phone, his household first, the parent approves before anything changes.
