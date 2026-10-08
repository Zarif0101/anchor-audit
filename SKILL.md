---
name: anchor-audit
description: Use whenever Zarif asks for content for his own brand or channels (posts, captions, scripts, video hooks, thumbnails, slides, landing pages, READMEs, code he'll publish). Drafts with specific input and a patch-only audit so the output reads like a particular person made it, not like default AI.
---

# anchor-audit

Content made with this skill should read as if one specific person made it, with an opinion and details only they would know. Removing tells is the floor. Specificity is the goal.

## Scope
- For Zarif's own brand and channels.
- Not for passing off AI work where human authorship is required (school work, exams, contracts, competitions with no-AI rules). If a request is that, say so and stop.
- Never promise "undetectable". Readers who use LLMs a lot catch AI text from originality as well as wording. The only real fix is real input.

## The six moves (apply while drafting)
1. Open on the specific thing: a number, a name, a place, a thing that happened.
2. One claim per sentence. Put the concrete noun early.
3. Vary sentence length on purpose. Some sentences are four words.
4. Take a position. Say what you'd bet on, and what you'd be wrong about.
5. Plain punctuation: periods, commas, the odd colon or parenthesis.
6. Stop when the point is made. No recap, no sign-off question.

Do not load `references/tells.md` while drafting. It is for the audit only, because naming a pattern while drafting makes it more likely to appear.

## State (outside this folder)
This skill folder is read-only. Keep state in `anchor-audit-state/` inside a connected folder (copy it from `state-template/` on first use). If there's no file access, run without state and say so in one line.
- `voice-corpus.md`: lines Zarif typed himself, verbatim, dated. Never add AI-written text.
- `log.md`: one line per piece.
- `last-moves.md`: the last 10 openers and audit moves used.

## Modes

### Lite (default, 0 minutes of his time)
One turn:
1. Read `last-moves.md` if available.
2. Draft with the six moves. If file tools exist, write the draft to `anchor-audit-state/drafts/<date>-<slug>.md`.
3. Read `references/audit.md` and `references/tells.md` and run the audit: change only the sentences that fail, by editing in place. Do not reprint the full draft twice.
4. Show the final piece once. Append to `log.md` and `last-moves.md`.

### Anchor (opt-in, about 5 minutes)
Use when he says "anchor", or when the piece is an opinion, story, or hook where his own line would carry it. Two turns total.

Turn 1, one message:
- Up to 3 questions picked from `references/intake-bank.md` for this medium, mixed differently each time.
- Then: "Type one line yourself: the hook or your opinion. Rough is fine. Or say 'lite'."

Turn 2:
1. Append his line verbatim to `voice-corpus.md` before anything else.
2. Read the last 5 corpus entries for register (word choice, sentence length, how he argues). Never copy them.
3. Draft around his line. Wrap his words in «» while working.
4. Audit as in Lite. Text inside «» is frozen: fix seams around it, never inside it.
5. Remove the «» markers, show the final once, and log the piece with mode=anchor and slot=y.

If he skips the questions or the line, run Lite without comment.

## Mediums
Load only the module you need: `references/text.md`, `references/design.md`, `references/video.md`, `references/code.md`. The modules for design, video and code are first drafts and haven't been tested.

## Language
English first. For Bangla, `tells.md` has no Bangla section yet. Flag the first Bangla piece so he can add one.

## Self-test
`eval/step0.md` has the 30-minute test that decides whether this skill earns its cost. Run it on first install and again after a model update.
