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



## BINDING: Analysis sequence (linguistic claim type)

Same method flow as Methodology (corpus → prepare → code appeal → code subtype → pair → Parts I–III). Claims are form/force/co-occurrence in CTA wording — not psychological effect. Prefer: worded as / realized through / coded as / co-occurs / pattern in the corpus. See decisions.md 2026-11-01 Analysis sequence stays linguistic.

## BINDING: BOTS literature (do not override)

For **all** Background of the Study themes, the gate is **method-fit**, not a fixed list of banned papers:

1. Do **not** reintroduce or add sources that pull the review off form–function analysis of CTA phrases (rhetorical appeals + directive subtypes).
2. Thicken only with on-topic **linguistic** sources that support that analysis.
3. Framing stays linguistic: appeals and subtypes are **realized / patterned** in CTA wording — not marketing effectiveness or "construction of persuasive meaning" as the main claim.

Examples of off-method drift (not exhaustive): engagement/effectiveness metrics, activism discourse, reactance, unrelated genres, consumer psychology without linguistic coding, brand ROI, ideology-only critique, platform algorithm mechanics, length-padding.

This rule is also recorded in `decisions.md` (2026-11-01). Prefer that entry if focus text conflicts.

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
Thesis revision: Ahlai Velasquez CTA Facebook skincare ads.
Working draft: `thesis/Velasquez_ThesisRevised_DRAFT_022.docx` (recode + frequencies + uncited drop + full ripple consistency pass).
BOTS Themes 1–6 restored full + citation-home map. Next: Chapter 1 after BOTS (Statement of the Problem, frameworks, Significance, Definition of Terms) with linguistic claim language. Binding: analysis sequence linguistic (decisions.md).

## Open threads
- Theme 1 locked into BOTS draft (dynamic version).
- Theme 2 locked (first dynamic version).
- Full formatting pass completed into DRAFT_004 (user-specified rules 2026-10-28).
- After Theme 2 is confirmed, proceed to remaining themes / integrate into main manuscript.
- Earlier Chapter 3 drafts in archive remain reference only unless user asks to merge.

## Recently completed
_Capped at 5 entries. Older items live in `decisions.md` and `chat_history/`._

- 2026-11-01: User uploaded `Velasquez_ThesisRevised_DRAFT_011.docx` as new base working draft (full manuscript). Set as current working file.

