# Current Context

Read this first after cloning.

## FIRST ACTION AT SESSION START

```sh
./scripts/new_session.sh [session_id] [YYYY-MM-DD] [model]
```

All args are optional. This creates `chat_history/<model>/<session_id>-<date>.md`
with the right header. The model defaults to `GLM`, so pass `Claude`,
`ChatGPT`, or whatever you are running as. Do this before anything else.

Then run `./scripts/doctor.sh` and fix any FAIL line before going on. Then
read `preferences.md` and `decisions.md`. Skim `knowledge.md` and
`projects.md` if the task touches them. If the session has been idle and
another session may have committed, run `GH_PAT=$GH_PAT ./scripts/sync_before_work.sh`
before editing.

## CRITICAL: log the user message BEFORE responding

Read `TRANSCRIPT_REMINDER.md` if you haven't. For every user message, before
you start the response:

```sh
echo "the user's message" | ./scripts/begin_exchange.sh <trace_id>
```

This appends the message with an `(in progress...)` marker for your reply.
Replace the marker with your reply when done. If the session truncates
before the log is written, the exchange is lost. Redact any token first.

The pre-commit hook blocks commits that change one of the six memory files
(listed under "Where things go") without a transcript update. CI warns on push. Docs, scripts, and
workflows aren't checked. Bypass with `--no-verify` only for commits
unrelated to the conversation.

## Where things go

Memory files are `preferences.md`, `knowledge.md`, `decisions.md`,
`lessons.md`, `context.md`, and `projects.md`.

- Facts go in `knowledge.md`.
- Preferences go in `preferences.md`.
- Durable decisions go in `decisions.md`.
- Mistakes and their fixes go in `lessons.md`. Never archived.
- Project state goes in `projects.md`.
- Verbatim record goes in `chat_history/`.
- This file holds only the current focus and open threads.

Before adding a lesson, fact, or decision, run `./scripts/search.sh <one
distinctive word>` and update the existing entry if there is one. Run it
also before solving a problem that feels familiar. When you use a saved
lesson, say so in your reply: `applied lesson: <title>`. Other retrieval
tools are described in `RETRIEVAL.md`.

## At session end

1. Promote anything durable from this session: mistakes and fixes to
   `lessons.md`, choices to `decisions.md`, facts to `knowledge.md`.
2. Refresh Current focus and Open threads below. Include what was tried and
   failed, so the next session doesn't repeat it.
3. Run `./scripts/doctor.sh`, fix any FAIL, then commit and push.

## Forgetting

To forget something, edit or delete the entry (or the transcript file) and
commit. Be clear with the user that git history still holds the old text,
and so does any fork or clone made earlier. If the text was a secret, revoke
or rotate it first. Rewriting history is a last resort and doesn't reach
copies already made.

## Current focus
Thesis revision: Ahlai Velasquez CTA Facebook skincare ads manuscript.
Primary file: `thesis/Velasquez_CTA_Skincare_Thesis_FINAL_2026-10-18.docx`.
Working draft: `thesis/Velasquez_CTA_Skincare_Thesis_DRAFT_003.docx` (from FINAL + polished BOTS). Full formatting pass applied (Georgia, double spacing, open table borders, bold-spill clear, uniform body spacing, margins A4, different_first_page).
Locked opening (Kemp 2025 + Desiderio 2026), Theme 1, Theme 2 dynamic versions now in the Background of the Study of DRAFT_003.
Next: confirm Theme 2 / proceed to Theme 3 or remaining integration and pagination polish if needed.

## Open threads
- Theme 1 locked into BOTS draft (dynamic version).
- Theme 2 locked (first dynamic version).
- After Theme 2 is confirmed, proceed to remaining themes / integrate into main manuscript.
- Earlier Chapter 3 drafts in archive remain reference only unless user asks to merge.

## Recently completed
_Capped at 5 entries. Older items live in `decisions.md` and `chat_history/`._

- 2026-10-28: Created DRAFT_003 from FINAL (preserves all images). Imported polished Background/theme content and structure from DRAFT_002 into it.
- 2026-10-28: Restored missing pagination (section headers + titlePg + first-page hide) and re-embedded referenced images into DRAFT_002 per companion + FORMATTING.md.
- 2026-10-28: Revised Theme 1 with varied paragraph shape/rhythm and folded into BOTS_Restructure_Draft_001.docx.
- 2026-10-28: Produced dynamic Theme 2 preview (kept separate; not locked).
- 2026-10-28: Verified all Theme 2 references as real; PDFs already present.
- 2026-10-28: Added binding FORMATTING.md, WRITING.md, BAELS Thesis Companion, Verb Tense Matrix.
- 2026-10-27: Created `thesis/` folder, uploaded FINAL Oct 18 manuscript, recovered prior drafts from thesis-memory into archive.

