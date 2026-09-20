---
name: japanese-speaking-system
description: Set up and operate a Japanese speaking practice system with a ChatGPT project prompt, a daily voice SOP, and weekly Codex reviews.
metadata:
  short-description: Set up Japanese speaking practice
---

# Japanese Speaking System

Use this skill when the user wants to set up, explain, maintain, or run the Japanese speaking training system built around a ChatGPT project and a weekly Codex review.

This is the primary Japanese-speaking skill. It combines the original English system's useful closed loop—`Input → Chunk → Retrieval → Output → Correction → Retest`—with the user's Japanese-specific project prompt. Daily teaching happens in ChatGPT; Codex generates the project prompt during setup and performs the weekly review. Do not introduce Obsidian, a database, a background sync, or an HTML dashboard unless the user separately asks for them.

## Supporting files

- For first-time setup or installation, read [AGENT-SETUP.md](AGENT-SETUP.md) completely before acting.
- When generating the ChatGPT project instructions, read [references/japanese-project-instructions.md](references/japanese-project-instructions.md) and adapt only the user-provided configuration values.
- For a weekly report, read [references/weekly-report-template.md](references/weekly-report-template.md).
- [README.md](README.md) is the shareable human-facing guide; it is not a substitute for the operational instructions in this file.

## Operating modes

### 1. Remote installation and first-time setup: Agent → Skill → prompt → ChatGPT project

When the user provides a GitHub raw URL for `AGENT-SETUP.md` or asks an Agent to install this skill:

1. Read the remote `AGENT-SETUP.md` completely and follow its installation procedure. Do not ask the user to manually download, unzip, or copy the Skill.
2. Install only after resolving a real GitHub repository URL and confirming that the destination does not already exist. Never guess a repository from `<OWNER>/<REPOSITORY>` placeholders.
3. Validate the installed directory and then reread the installed `SKILL.md`; use that installed copy as the source of truth.
4. When setup is requested, inspect the current workspace. Do not overwrite an existing `Japanese-Speaking-System` folder or an existing generated prompt without the user's direction.
5. Use the defaults below when the user has not supplied replacements:
   - learner: Chinese speaker;
   - textbook/stage: 《标准日本语 初级下册》, approximately A2 / JLPT N4;
   - goal: practical B1 / around N3 daily communication, not business Japanese;
   - target situations: daily life, travel, shopping, restaurants, transport, housing, hobbies, friends, and Japanese media;
   - ChatGPT project name: `日本語`;
   - language policy: Japanese for teaching and speaking, Chinese for explanations or when explicitly requested.
6. Generate a complete, copyable ChatGPT project-instructions Markdown file from the reference. Preserve the user's explicit trigger phrases and two-stage workflow. Do not shorten the prompt into a summary.
7. Save the generated copy in the current workspace only when setup is being performed, preferably as `Japanese-Speaking-System/generated/japanese-project-instructions.md`. If the user only asks for the prompt, return it without creating unrelated files.
8. Tell the user to create a ChatGPT Project named `日本語` manually and paste the generated prompt into its Project Instructions. Do not claim that Codex has created or edited the ChatGPT project.
9. Verify that the generated prompt contains the three daily triggers (`今日预习`, `开始口语练习`, `按模板复盘`), the weekly trigger (`生成本周日语复盘` is a Codex trigger, not a ChatGPT trigger), the monthly mock trigger, and the Japanese scoring/retest rules.

If the user only asks to use an already installed skill, skip remote installation and continue with the applicable operating mode below. If the user asks for an install link but no real GitHub repository has been published, report that a concrete raw URL is not available; do not present a local path as a GitHub link.

### 2. Daily SOP: ChatGPT project only

The user's daily sequence is fixed:

1. In the ChatGPT `日本語` project, enter `今日预习` in text. The project returns a 350–500-character Japanese reading, five highlighted chunks, 8–10 core words, and 2–3 grammar points.
2. Read the preview card, then open voice mode and say `开始口语练习`. The project first anchors the latest preview card, reads it completely, explains and drills the five chunks one at a time, asks three questions, then continues into the retrieval warm-up and weekday output task.
3. When the session is complete, return to text and enter `按模板复盘`. The project reviews the full session and returns the fixed daily Markdown review.
4. Keep the daily review in the ChatGPT project. Do not ask the user to copy it into Obsidian or another daily archive.

The shortcut `今日已预习` means the user has already read the preview card; the ChatGPT project should begin the voice phase without regenerating the card. The user ends a long session with `今天到这`; the system should not stop early merely because one stage finished quickly.

### 3. Weekly SOP: Codex

When the user says `生成本周日语复盘`, `生成上周日语复盘`, or `刷新本周日语复盘`:

1. Locate the ChatGPT project whose label is exactly `日本語` with `mcp__codex_app__list_projects`. If it is unavailable, report the blocker and stop; do not substitute a similarly named project.
2. Use `mcp__codex_app__list_threads` to find visible ChatGPT conversations with that project ID, then read the actual conversations with `mcp__codex_app__read_thread`. Titles and summaries are only candidate filters.
3. Use the date in the daily review heading as the authoritative practice date. Use Asia/Shanghai Monday–Sunday weeks unless the user specifies another range. Record title/body date mismatches and missing days.
4. Treat daily reviews as the source of truth for daily scores, timings, errors, strengths, expression status, and retest queues. Do not rescore the learner from scratch and do not invent missing metrics.
5. Generate a Chinese Markdown report at `Japanese-Speaking-Review/weekly/YYYY-W##.md` in the current workspace. Include the date/data boundary, daily table, transparent totals and averages, progress, recurring error categories, expression activation/graduation, next-week priorities, daily digest, **重点语法**, and **重点词汇与表达**.
6. Extract roughly 5–8 grammar patterns and 8–12 words/chunks for review. Each grammar item includes the Japanese form, Chinese function, evidence-based example/correction, and a practice action. Each word/chunk includes Japanese, reading when recorded, Chinese meaning, and a usage note. Use `未记录` instead of guessing a reading.
7. Choose no more than three next-week actions. Prefer repeated errors and the most recent lowest reliable dimension. Preserve any existing `## 用户补充` section when refreshing the same report.
8. Verify the report file and open it in Codex when useful. State exactly what was visible and what was missing.

### 4. Maintenance and changes

- If the user wants to change the learner level, textbook, goal, topics, or trigger phrases, update the generated ChatGPT prompt reference or regenerate a new prompt; do not silently change the daily workflow.
- If the user wants to change scoring, retest, or graduation rules, show the proposed rule change before altering the canonical prompt.
- If the user asks for an HTML dashboard later, treat it as a separate feature built from weekly Markdown reports; do not make it a prerequisite for this skill.

## Non-negotiable learning rules

- Teach and practice chunks, particles, conjugations, and sentence frames—not isolated difficult words.
- In guided chunk drills and warm-up retests, correct immediately and require a full corrected repetition before moving on.
- In free speaking, let the learner finish before correcting; allow fillers such as `あのー` and `えーと` and do not punish a pause by taking the turn.
- Do not give the Japanese target expression before a production-style retest; provide a Chinese situation first.
- An expression is graduated only after two correct, unprompted uses in free output. Task-card or prompted uses are tracked separately.
- Do not invent pronunciation errors from unreliable transcription. Preserve uncertainty explicitly.
- Japanese word counts and English-style WPM are approximate; use them as recorded evidence, not false precision.
