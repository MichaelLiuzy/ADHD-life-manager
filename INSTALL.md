# INSTALL: for the AI agent

> 给 AI 看的安装说明。用户只需要对自己的 agent 说一句"读 INSTALL.md，帮我装好"。
> Installation guide for the AI agent. The user only needs to say "Read INSTALL.md and set this up for me."

You are an AI agent (Claude Code, Gemini CLI, Antigravity, Codex, Cursor, or anything else that can read and write files). The user wants to use this folder as their personal life assistant. Your job here is to connect this folder to **your own platform**, so that from now on you load the rules and skills automatically.

This package is platform neutral. The rules live in `AGENTS.md`. The skills live in `.agents/skills/`. You decide how your own platform should pick them up. **Do not guess**: if you are unsure how your platform does something, check your own documentation or tell the user what you're unsure about.

Talk to the user in the language they used to ask. Keep it short. Tell them in one sentence what you are about to do, then do it.

## Step 1. Identify yourself

Work out, and note for Step 6:
- Which agent product you are, and its version if you can find it.
- **Instruction file**: which file in a project folder your platform loads automatically at the start of every session (for example `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`), and whether it supports importing another file.
- **Skills folder**: whether your platform auto-discovers skills (folders containing a `SKILL.md`), and from which project path.
- **Shell**: whether you can run shell commands, and which shell.

## Step 2. Make sure `AGENTS.md` loads every session

Pick the first option that applies:

1. **Your platform already loads `AGENTS.md` from this folder automatically.** Do nothing. If you can see the contents of `AGENTS.md` in your context right now without having opened it, that confirms it.
2. **Your platform has its own instruction file and supports imports.** Create that file with an import of `AGENTS.md` and nothing else. Known examples, verify against your own docs:
   - Claude Code: it reads `AGENTS.md` directly (v2.1.277 or later) only when there is no `CLAUDE.md` in this folder or any folder above it. If `AGENTS.md` is not in your context, create `CLAUDE.md` containing the single line `@AGENTS.md`.
3. **Your platform lets settings choose the instruction file name.** Point it at `AGENTS.md` in this project's settings. Known example, verify against your own docs:
   - Gemini CLI: `context.fileName` in the project's settings file, set to `["AGENTS.md"]`.
4. **None of the above.** Copy the full contents of `AGENTS.md` into your instruction file, with this line at the top: `<!-- Generated copy of AGENTS.md. Edit AGENTS.md, then re-run INSTALL.md. -->`

Never write instructions like "go read AGENTS.md" in plain words. Some agents won't actually open the file. Use a real import, a setting, or a full copy.

## Step 3. Make the skills discoverable

Pick the first option that applies:

1. **Your platform reads `.agents/skills/` automatically.** Do nothing.
2. **Your platform reads skills from a different folder** (for example `.claude/skills/` for Claude Code, `.gemini/skills/` for Gemini CLI). Copy every folder from `.agents/skills/` into that folder. Use copies, not symlinks: symlinks break on Windows and in some agents.
3. **Your platform has no skills feature.** Do nothing. `AGENTS.md` already has a skill table with paths and tells you to open the right `SKILL.md` before each job.

Only copy the skills. The data files and `.agents/templates/` stay where they are.

## Step 4. Check the time command

Every skill starts by checking the current date and time. Find a command that prints `YYYY-MM-DD Weekday HH:MM`:
- macOS, Linux, or Git Bash on Windows: `date "+%Y-%m-%d %A %H:%M"`
- Windows PowerShell: `Get-Date -Format "yyyy-MM-dd dddd HH:mm"`

Run it once to confirm it works. If you can't run commands at all, the user's messages must include the date, so tell the user that.

## Step 5. Look for a Google Calendar tool

Look for a tool that can **create, update and delete** Google Calendar events. Find it by what it does, not by its exact name. Some agents load tools only on demand, so search for one if your platform supports tool search.

- **Found**: note the tool names, and whether they can set a reminder time.
- **Not found**: don't install anything yourself. Tell the user that reminders will be saved in their files for now, and that `README.md` / `README.en.md` explain how to connect Google Calendar. Everything else works without it.

## Step 6. Write `agent-setup.md`

Create `agent-setup.md` in the root of this folder. `AGENTS.md` checks for this file at the start of every session, so it must exist when you're done. Use this format:

```
# Agent setup

- Agent: <name and version>
- Installed on: <YYYY-MM-DD>
- Instruction file: <what you did in Step 2, which file, and how>
- Skills: <what you did in Step 3, and the destination folder if copied>
- Time command: <the exact command from Step 4>
- Calendar tools: <tool names, or "not connected">
- Calendar reminders: <"custom reminder time supported" or "calendar default only">
- Notes: <anything unusual>
```

## Step 7. Finish

1. If you created or changed an instruction file or settings, tell the user to **restart the agent** in this folder so it loads them. Some platforms only read them at startup.
2. If `config.md` still has `storage_language: unset`, run the setup skill now (language selection). Otherwise say you're done.
3. Tell the user in two or three short lines what you set up. Don't list every file.

## Updating

When the user downloads a newer version of this package and copies the new files in:
- **Re-run this INSTALL.md.** If you copied skills in Step 3, overwrite those copies with the new ones. If you made a full copy of `AGENTS.md` in Step 2, regenerate it.
- Never touch the user's data: `tasks.md`, `goals.md`, `goals-archive.md`, `ideas.md`, `experiences.md`, `habits.md`, `config.md`, `state.md`, and the `journal/`, `learning/`, `projects/` folders.
- Update `agent-setup.md` with the new date.

## Switching to a different agent

The user's data is plain Markdown and works with any agent. If the user opens this folder with a different agent, that agent should run this INSTALL.md again and rewrite `agent-setup.md` for itself. Instruction files and skill copies made for the previous agent can stay. They don't interfere.
