# 设置 Settings

可以直接改这个文件，也可以让助理帮你改。
You can edit this file directly, or ask the assistant to change it.

## 语言 Language

显示语言 display_language: unset
存储语言 storage_language: unset

<!--
display_language: zh / en / auto（auto = 跟随用户每句话的语言 follow each message）
storage_language: zh / en。设置后锁定，要换请说"把数据转成英文/中文"。
Locked once set. To change it, say "convert my data to Chinese/English".
-->

## 回顾 Review

周回顾日 review_day: Sunday

## 日历 Calendar

同步到 Google 日历 sync_google_calendar: yes
日历ID calendar_id: primary
默认提前提醒分钟数 default_reminder_minutes: 10
有具体时间的任务默认时长分钟数 default_event_minutes: 30
自动提醒 auto_remind: timed, deadlines
截止提醒时间 deadline_reminder_time: 09:00

<!--
auto_remind：哪些任务不用我说"提醒我"也自动建日历提醒。
  timed = 有具体钟点的任务；deadlines = 必须且有截止日的任务（截止前一天提醒）。
  两个都要写 "timed, deadlines"；都不要写 "none"。
auto_remind: which tasks get a calendar reminder without asking.
  timed = tasks with an exact time; deadlines = must-do tasks with a due date (reminded the day before).
-->

## 学习 Learning

默认复盘频率 default_retro_every: 1 month

<!--
学习档案多久复盘一次。可选 1 week / 2 weeks / 1 month / 2 months / 1 quarter。
复盘只在对话里提醒，不建日历事件。
How often to do a retro on each skill. Retros are only mentioned in chat, never added to the calendar.
-->

## 个人风格 Personal style

<!--
可选。写在这里的规则会加到 AGENTS.md 的回答风格里。每行一条。
Optional. Rules here are added to the reply style in AGENTS.md. One per line.
例 e.g.:
- 不用破折号
- Keep every reply under 5 lines
-->
