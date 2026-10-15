# Life Assistant

[中文](README.md)

A personal life assistant that runs inside an AI agent. You talk the way you think. It sorts things out, files them, reminds you, and when you ask "what now?" it gives you one answer.

Built for an ADHD-shaped life: lots of ideas, uneven energy, and plans that change on the fly.

It isn't tied to any one AI tool. Claude Code, Gemini, Antigravity, Codex, or any agent that can read and write files can run it.

> **Note for AI agents**: if you're an AI agent reading this folder and there's no `agent-setup.md` yet, follow `INSTALL.md` first. Once installed, all the rules are in `AGENTS.md`. This README is for humans.

## Highlights

- **Just talk.** "Want to do laundry today, groceries this afternoon, and I have to finish that movie by Saturday." It splits that into separate items, ranks them as must, plan or maybe, and files them under today, this week, or your idea pile.
- **It only asks when it's unsure.** When capturing, it flags at most three things it can't decide. Reply "ok" and it's saved.
- **"What now?" gets one answer.** No wall of tasks. Ask for the full list when you want it.
- **Plans can shrink anytime.** Say "I can't today" and it keeps the single most important thing and moves the rest. No questions about why.
- **It notices what keeps slipping.** If something gets pushed three times, it asks whether to break it down, push it further out, or let it go.
- **Ideas are kept, not forced.** Anything without a time goes into your idea pile. The weekly review brings a few back now and then.
- **Four layers of goals.** Year, quarter, month, this week. Whenever planning mood strikes, it sorts your thoughts into layers and breaks them into tasks you can start right away.
- **A five-minute weekly review.** What got done, what keeps getting pushed, how your habits and goals are going, then pick next week's focus. Month, quarter and year reviews happen automatically when a period ends.
- **A log for each skill you're learning.** Boxing, drawing, fiction writing: each gets its own file. When you started, what you practiced each time, and how far along you are at each retro. Retros default to once a month, can be set per skill, and are only mentioned in chat, never added to your calendar.
- **A log for each long-running project.** A novel, an app, a board game: each project gets its own file with next steps, milestones, a progress log and notes. Track progress with a number if you like, such as word count. Projects untouched for two weeks get flagged.
- **Mark it done once, it lands everywhere.** "Finished the book" goes into your journal and your reading log. "Worked out" also checks off your habit.
- **Reminders on your phone.** Once Google Calendar is connected, tasks with an exact time and must-do tasks with a due date get calendar reminders automatically. No need to ask.
- **Chinese or English.** Pick one at first launch and switch anytime. Data is stored in one consistent format, never mixed.
- **Your data stays yours.** Everything is plain text in this folder. Open it, edit it, take it anywhere, even to a different AI tool.

## Getting started

1. Have an AI agent that can read and write local files, such as Claude Code, Gemini CLI, Antigravity or Codex.
2. Launch it inside this folder.
3. Tell it: **"Read INSTALL.md and set this up for me."**
   It figures out how to hook the rules and skills into itself, then asks you to pick a language: English, Chinese, or auto.
4. If it asks you to restart, quit and open it again.
5. Say hi. It'll tell you what you can do.

Always launch your agent from inside this folder. Otherwise it can't see the rules or your data.

## Things you can say

| You say | It does |
|---|---|
| A messy list of things to do or try | Splits, sorts, asks you to confirm |
| What now? | Suggests one thing based on the time |
| What's today / this week / everything | Lists by time range |
| Paid rent / finished it / worked out today | Logs it and files it everywhere it belongs |
| I can't today | Keeps one thing, moves the rest |
| Help me plan / this month I want to... | Organizes it into four layers of goals |
| Review | Weekly review and next week's focus |
| Started boxing / practiced boxing today | Creates a learning log / logs a session |
| Retro on boxing / how's my learning going | Looks back on progress / shows the learning curve |
| Do boxing retros every 2 weeks | Changes the retro frequency |
| Started my novel / wrote 2000 words today | Creates a project log / logs progress |
| What's next for my novel / my projects | Shows next steps / shows all project progress |
| Sync calendar | Checks and fills in calendar reminders |
| Switch to Chinese / auto | Changes the reply language |
| Convert my data to Chinese | Rewrites all data in Chinese format |

## Files

Right after download, there's only this:

| File | What's inside |
|---|---|
| `README.md` / `README.en.md` | This guide |
| `INSTALL.md` | Install instructions for the AI |
| `AGENTS.md` | The assistant's rules. Its brain |
| `config.md` | Settings: language, review day, calendar, personal style |
| `.agents/` | Skills and blank templates. A hidden folder you can ignore |

After install and language setup, you'll also have:

| File | What's inside |
|---|---|
| `tasks.md` | Active tasks |
| `goals.md` | Four layers of goals |
| `ideas.md` | Idea pile |
| `experiences.md` | Books, films, shows, albums, live shows and cities you want to try or have done |
| `habits.md` | Habit definitions and log |
| `journal/` | One file per month: finished items and weekly reviews |
| `learning/` | Skills you're learning, one file per skill |
| `projects/` | Long-running projects, one file per project |
| `state.md` | System state. Leave it alone |
| `agent-setup.md` | Install record: which agent, what it changed |

After a while, `goals-archive.md` also appears, holding past goals and how they went.

Your agent may also create a file or two it needs for itself, such as a `.claude/` folder or `CLAUDE.md` for Claude Code. These are all listed in `agent-setup.md`.

On a Mac, press `Cmd + Shift + .` in Finder to see hidden folders.

## Language

- **Reply language**: English, Chinese, or follow whatever language you use in each message. Change it anytime by asking.
- **Storage language**: the format used for fields in your data files. It's set once at first launch and stays fixed. Your own words (task names, ideas, thoughts) are kept exactly as you wrote them, never translated.
- To switch the storage format, say "convert my data to Chinese" or "to English". It rewrites every file.

## Connecting Google Calendar

Each agent connects differently. Two examples below. Check your tool's own docs for the details.

**Claude Code**: you need a paid Claude plan, logged into Claude Code with that account. In Claude on the web or desktop, open Settings, go to Connectors, add Google Calendar and sign in. Back in Claude Code, type `/mcp` and check that it shows as connected.

**Gemini CLI**: install Google's official Workspace extension:
```
gemini extensions install https://github.com/gemini-cli-extensions/workspace
```

**Other agents**: look for Google Calendar in its extensions, plugins or MCP list.

Once connected, say "sync calendar" to fill in reminders saved earlier. From then on, tasks with an exact time, a reminder, or a must-do due date sync automatically. With the Google Calendar app on your phone, you'll get notifications on time.

- Choose which tasks get automatic reminders with `auto_remind` in `config.md`.
- The first time it creates an event, your agent may ask whether to allow the calendar tool. Choose always allow so it won't ask again.
- To turn syncing off, set `sync_google_calendar` to `no` in `config.md`.
- It works fine without a calendar. Reminders are kept in your tasks.

## Updating

1. Back up the whole folder first.
2. Replace `README.md`, `README.en.md`, `INSTALL.md`, `AGENTS.md` and `.agents/` with the new versions.
3. Don't overwrite your data files or `config.md`.
4. Tell your agent "run INSTALL.md again". It refreshes its own copy of the skills.

## Privacy

- All data lives in this folder on your computer.
- The assistant only touches calendar events it created. Your other events are left alone.
- Conversations are sent to the AI provider behind your agent, the same as any other use of that tool.
