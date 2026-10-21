# Everyarc — ADR 002: Alpha-grade outcomes at home
*Decided by Hew, 2026-10-10. Supersedes the lines named under "What changes" in `everyarc-curriculum-handling.md`, `everyarc-semantics-and-feedback.md`, `everyarc-kid-design-brief.md` and `CLAUDE.md`. Everything else in those docs, and every other doc, stands.*
*v0.1 · 2026-10-10 · Shared. Change it through this doc's changelog.*

---

## Decision
Everyarc is built to deliver at home what Alpha School's "2 Hour Learning" delivers in its schools: **mastery-based, adaptive 1:1 practice that moves a child about twice as fast through the material**, in a bounded daily block, with a person as the guide and the rest of the day for life. Four calls make that concrete:

1. **Pace, in school-years, never against other children.** Parents see how fast their own child is moving through the material: "about a school year's worth of the math Everyarc covers, in 5 months." Growth stays self-referenced: no percentiles, no national norms, no peers, no grade-level headlines. Kids still see no numbers.
2. **A daily target the parent sets, in focus blocks.** Default 45 minutes, up to 2 hours, made of focus blocks of about 25 minutes with real breaks between them. The child sees time as their arc filling, and can tap to see minutes. Never a countdown on a question, never a word about speed.
3. **Family goals with real-world rewards.** The parent sets a goal (time on target this week, skills made solid) and a reward from real life ("pick Friday's movie"). The app tracks progress and explains the deal to the child. No in-app currency, points, streaks or prizes.
4. **Math K–8 first, then reading.** The math slice grows from grades 2–5 to K–8 so it can actually carry a child two years in one; reading and writing follow. Life skills arrive as parent-led "afternoon" missions through home support.

## Why
- **The core already matches.** Alpha advances a student after 90% mastery of a concept; Everyarc's fluency gate is 90% on first tries, spread over days and ways (curriculum handling §1.1). Alpha has no ceiling and groups by what a child shows, not age; so does Everyarc (eligibility follows evidence). Alpha uses AI software for practice and people for mentoring; in Everyarc the child never talks to a model, and the parent is the guide, coached weekly by the home support card.
- **The gap at home is real.** Alpha's own at-home option, Alpha Anywhere, is paused through the end of 2026 (alpha.school/faq, read 2026-10-10). Families who want this model and can't reach a campus have nowhere to go.
- **The four calls keep what makes Everyarc trustworthy.** Pace replaces Alpha's norm-referenced claims without ranking a child against anyone; a parent-set target replaces a fixed 2-hour day that would be heavy for a school-day supplement; family goals keep motivation in the family's hands instead of an app's economy.

## What changes

| Doc and line | Before | Now |
|---|---|---|
| Curriculum handling §2, session length | 8–10 · 12–15 · 15–20 minutes by age; "the app never asks for a second session" | A **daily target** set by the parent (default 45 minutes, up to 120), in **focus blocks** of about 25 minutes (shorter for ages 5–7: about 15) with breaks of 3–5 minutes between them. Each block keeps the session arc (arrive, warm up, core, choice, close) and ends well. The app still never asks for more than the parent's target, and stopping is always fine |
| Curriculum handling §3.1, "never" column | No timers; nothing about pace | Still no timer on a question and nothing about speed. **New:** the day's time shows as the child's arc filling toward the target, tappable to see minutes. It is a picture of their own day, never a race |
| Semantics §4.6, growth first | Counts only | Counts, plus **pace in school-years of the material Everyarc covers**, once there are at least 10 sessions; always "the math Everyarc covers", never "a school year of math", never against another child, a grade's average or a norm |
| Kid design brief §15 and CLAUDE.md "what not to build" | No points, currencies or collections | Unchanged. **New:** family goals with a reward the parent chooses from real life, tracked without a currency |
| CLAUDE.md principle 3 | No percentages for skills | Unchanged. Pace is in school-years and months, never a percentage |
| Scope (README, build spec "What v1 is") | Grades 2–5 math | Beta stays grades 2–5 math; **then math K–8**, then reading and writing |

## What doesn't change
The three zones and the bridge; the fluency bar (90% first go, 92% after a drop) and silent drops; self-referenced growth; the child never talks to a model; no streaks, no leaderboards, no sibling comparison; strengths first; dignity; calm, not sticky; every other rule in `CLAUDE.md`.

## Not claimed
Everyarc does not claim "2x" or any efficacy number until its own families' data shows it, measured honestly [BP §22.4]. The parent-language validator rejects efficacy claims ("twice as fast", "2x") in anything a parent reads.

## Contract proposals this needs (bridge §13; adopted in principle by this ADR, shape to confirm)
- **P4 · rhythm:** `daily_target_minutes` (15–120) and `block_minutes` (10–30) in the brief's `rhythm`, reaching the iPad as session settings (§6.1). Minor, additive.
- **P5 · family goals:** a presentation field for the iPad: the goal's kind (`minutes_this_week` | `skills_solid`), its target, and the reward in the parent's words (a † free-text field through the filter, ≤ 80 characters, shown, never spoken). Widens what reaches a device, so it needs this sign-off.

## Revisit when
The first families' data shows the daily target is too heavy or too light by age; parents ask for norm-referenced outside assessment (a MAP-style test can be added as a *documented* source in M5 without changing what the app itself claims).

## Changelog
- **v0.1 · 2026-10-10 · Hew's decision:** Alpha-grade outcomes at home: pace in school-years, a parent-set daily target in focus blocks, family goals with real rewards, math K–8 then reading.
- **2026-10-10 · Hew's decision (ADR 003 v0.2):** the fluency bar under "What doesn't change" is now 100% (20 of 20, the same after a drop); see `everyarc-adr-003-high-support-high-performance.md`. P4 and P5 built in turn 4b.
