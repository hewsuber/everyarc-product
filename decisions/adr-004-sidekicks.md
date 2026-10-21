# Everyarc — ADR 004: Sidekicks
*Decided by Hew, 2026-10-20. Supersedes the lines named under "What changes" in `everyarc-kid-design-brief.md`, `everyarc-kid-image-bank.md`, `everyarc-voice-and-sound.md`, `everyarc-semantics-and-feedback.md`, `everyarc-bridge-contract.md` and `CLAUDE.md`. Everything else in those docs, and every other doc, stands.*
*v0.1 · 2026-10-20 · Shared. Change it through this doc's changelog. The build brief is `everyarc-claude-code-sidekicks.md` (v0.1.1); where it and this ADR disagree about where the sidekick sits, this ADR wins.*

---

## Decision
Everyarc Kids gets **sidekicks**: three illustrated characters a child can pick, drawn from Hew's sheets in `_character_design/`.
- **Clementine:** a girl of about nine or ten, with curly dark hair and round red glasses.
- **Bamboo:** a panda.
- **Squeak:** a gray mouse.

The sidekick reads aloud in its own voice, and looks at and points to the part of the work that matters. A child can pick one, or "just a voice". All three are equals: no main character, no default pick, never ranked. They are the only characters in Everyarc that speak.

### Where it sits
- **A circle hovering over the child's world**, at one of eight points: the four corners, the middle of the left and right edges, and the centre of the top and bottom edges. It starts bottom-right.
- **The child drags it to any point**, and it eases into place: `glide`, easing out, nothing elastic.
- **Three sizes:** full; a peek, its head in an 88 pt circle; and hidden, where its voice keeps reading.
- **The choice is remembered per child.** A tap on the circle replays the last line. The pause sheet and Make it mine (K19) offer the same placement and size as plain controls, for anyone who doesn't drag.
- **The work makes room.** Wherever the circle sits, that screen moves what's there (the card, the help rail, the chips, the header), so nothing tappable or readable is ever under it. The move eases along with the circle. While a child drags a piece on a Flashboard, the sidekick shrinks to a peek on its own, and the work doesn't move.
- **It faces the work.** The sheets face right. Whether the sidekick is mirrored follows where the circle sits relative to the work, not which edge it's on.

### Rules
1. **A character, never a companion.**
   - A sidekick speaks only reviewed phrase-bank lines and validated item text.
   - No chat and no generated lines. Never "I".
   - It never claims feelings, friendship, memory or needs, and never mentions absence ("missed you", "come back"). No secrets and no persuasion [BP §18.4].
   - It introduces itself without "I": "Hi. Squeak here."
2. **Still while the child thinks.** While an item is active and the child hasn't acted, the sidekick holds still with its eyes on the work. Its only motion is a slow blink every 6–10 seconds: the one exception to "nothing moves while a child is thinking". It acts at moments, then settles.
3. **Never over the work, never louder than the work.**
   - The work makes room, as above. Captions stay under the work, with the sidekick pointing to them.
   - No cheering, jumping, confetti or celebration theater: a milestone gets a warm smile and a nod.
   - Never sad, frowning, disappointed or impatient. No shake on a miss, and no red on anything about the work. Clementine's red glasses are a character color, never a feedback color.
4. **The child chooses.** They pick a sidekick or "just a voice" in Make it yours (K4) and Make it mine (K19), and move, shrink or hide it. Nothing is pre-selected, and changing it is free and silent.
5. **The parent decides whether.** `sidekicks_allowed` in the plan: all three (the default), some, or none. A brief without it means no sidekick. The parent sees the child's sidekick in the portal preview.
6. **Private by construction.**
   - All animation runs on the iPad from shipped art and cue files.
   - No camera, microphone, face tracking or eye tracking, ever. The sidekick "looks at the child" by pose, not by sensing.
   - Nothing personal is voiced, and the nickname is never spoken.
7. **Calm mode, reduced motion, siblings.**
   - **Calm mode:** the sidekick stays, in its own voice; it drops gestures and only breathes and blinks.
   - **Reduced motion:** no body motion; the mouth uses only its three plainest shapes; blinks stay.
   - **Siblings on a shared iPad:** each child's sidekick is theirs. On a profile switch the old one waves goodbye and the next child's arrives. Profile cards (K3) show marks, never sidekicks.
8. **Drawn with care.**
   - Clementine's curls, skin and features are drawn and animated with care: curls in clusters, never one blob, and no caricature.
   - Every sidekick asset passes the image bank's review checklist (§4), with its provenance recorded in `sidekicks/PROVENANCE.md`.

## Why
- **Characters help, a little, especially children.** On-screen characters ("pedagogical agents") give a small but real learning boost, larger for K–12 learners than for adults (Schroeder, Adesope and Gilbert, 2013: 43 studies).
- **Connection and response matter.** Children aged 3–6 who felt a stronger connection to a character learned more math from it, and transfer was stronger with an embodied character that responded to them (Calvert and others, *Child Development*, 2019).
- **The face alone doesn't do it.** Human-like gaze, gesture and expression do (Mayer's social-cue principles). So a sidekick's job is **attention, not decoration**: it looks at and points to what matters, and is otherwise still. It responds to what the child *does*, never to what they say. The child still never talks to a model.
- **Why "sidekick":** ADR 002 already uses "guide" for the parent, and "companion", "friend" and "buddy" frame attachment [BP §18.4]. The child is the hero; the sidekick helps.

## What changes

| Doc and line | Before | Now |
|---|---|---|
| Kid design brief §4, layout | One help rail, always in the same place; the child's chips in one corner | The sidekick's circle reserves its point in every layout, and the work makes room. The help rail flips to the left edge while the circle sits at the right middle, and returns when it moves. Chips slide or wrap. The caption sits in the widest free stretch of the bottom band |
| Kid design brief §5, screens | No sidekick | K4 and K19: "Pick your sidekick" (three full-body cards from the sheets, plus "Just a voice"; tapping a card plays that sidekick's intro line). K19 and the pause sheet also hold placement and size. K6: an arrival wave once a session. K13 and K14: the sidekick breathes with the arc. K3: marks only |
| Kid design brief §7, motion | "Nothing moves while a child is thinking, except what their own hands are doing" | Unchanged, with one exception: a sidekick's slow blink every 6–10 seconds |
| Kid design brief §9, text and voice | The child's reading voice reads | With a sidekick, the sidekick's own voice reads. Captions are unchanged |
| Kid design brief §10 and §15, limits and never | "No character cheering; no mascot"; never "a mascot, a character that speaks" | Exactly three sidekicks, the only characters that speak, under the rules above. Still no character cheering, and no other character |
| Kid design brief §12, imagery | People are "never a mascot, never a guide, never speaking" | A third kind of image: sidekicks, drawn from Hew's sheets. People in story scenes stay silent and never guide |
| Image bank §2, AVOID | "No mascots or cartoon faces" | Sidekicks are excepted: their own set from Hew's sheets, never generated variants. §6.5 is unchanged |
| Voice and sound §2, §5 and §7.1 | Five voices plus one for later. The bootstrap lives in `audio/`, with schemas in `contract/audio/` | Plus three sidekick voices: `clementine`, `bamboo` and `squeak`. With a sidekick, calm mode keeps that sidekick's voice, so a voice never changes mid-session. Costs are updated. The bootstrap lives in `scripts/audio` (TypeScript) and its schemas in `contract/schemas/` |
| Semantics §6.2, item 9 | "The voice is a calm guide, not a character with feelings" | "The voice is a calm guide. A sidekick is a character that never claims feelings." Never "I" and no names aloud stay as they are |
| CLAUDE.md | No sidekick | Vocabulary: **Sidekick**. What not to build: a character that converses with a child |
| Bridge contract | No sidekick | P14, P15 and P16 below |

## What doesn't change
- The child never talks to a model. Never "I"; no names spoken.
- No streaks, points or currencies. Calm, not sticky.
- The three zones and the bridge. Every other rule in `CLAUDE.md`.

## Not claimed
Nothing a parent reads says sidekicks help learning until Everyarc's own families show it. The parent-language validator rejects that claim, as it rejects "2x" (ADR 002).

**How we'll know:** turn 16's pilot runs sidekick against voice only.
- **Design:** randomized by household (never between siblings), for 4–6 weeks.
- **Measured:**
  - skills newly shown independently;
  - focus blocks completed;
  - sessions ended by the stop rule rather than abandoned;
  - hint use;
  - children's own preference (asked, never inferred);
  - parents' concerns.
- **Never measured:** time in the app.

## Contract proposals this needs (bridge §13; signed off with this ADR on 2026-10-20)
- **P14 · sidekicks:**
  - `sidekicks_allowed` (sidekick ids from the manifest) in the brief's boundaries and the presentation fields. Absent or empty means none.
  - `sidekicks` in the manifest: `sidekick_id`, `name`, `voice`, `rig_version`.
  - `portal_choice` gains `sidekick` (an id or `none`), `sidekick_anchor` (`tl`, `t`, `tr`, `r`, `br`, `b`, `bl`, `l`) and `sidekick_size` (`full`, `peek`, `hidden`).
  - The truth line counts them ("3 sidekicks").
  - Minor, additive.
- **P15 · portal config on the iPad:** the child's portal choices reach their iPad as a presentation field, as §6.1 already lists, so a child's sidekick and its place survive a re-pair. Nothing new is exposed.
- **P16 · the iPad's own progress:** `device_progress` returns the day's and week's minutes, family goal progress, the child's marks and coverage edges, for My Arc (K18) and the arc filling. The data is the child's own; nothing about any other child.
- **Home-internal:** a proposal carries the iPad's own id, so a retry after a lost response never raises a second alert.

## Revisit when
- The experiment shows no benefit.
- Children or parents find the sidekicks distracting.
- Any sign of attachment framing.

## Changelog
- **v0.1 · 2026-10-20 · Hew's decision:** three sidekicks, the circle at eight points, and the work makes room; P14 to P16 signed off.
- **v0.1 · 2026-10-20 · Hew approved the art (Stop 1):** Clementine, Bamboo and Squeak, rebuilt from his sheets, replace the stand-in everywhere; drawn flat (A-91). The manifest offers all three (rig 1), so a plan allows them by default, and the parent's plan now has the control for some or none (rule 5).
