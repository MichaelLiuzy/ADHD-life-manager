---
name: setup
description: 首次使用时选择语言并建立数据文件；之后切换显示语言，或把全部数据转换成另一种存储语言。First-run language setup, switching the display language, or converting all data to another storage language. Triggers include "切换语言"、"说英文"、"把数据转成英文"、"change language"、"switch to Chinese"、"convert my data to English".
---

# 设置

## 情况一：首次使用

`config.md` 里 `storage_language` 是 `unset` 时运行。

### 1. 先看有没有旧数据

检查根目录有没有 `tasks.md`、`goals.md`、`ideas.md`、`experiences.md`、`habits.md`。

**有旧数据**（老版本升级上来的）：读里面的字段写法，判断是中文还是英文，直接把 `storage_language` 设成那种语言，不问用户。缺的文件从对应模板补上。然后只问显示语言，跳到第 3 步。

**没有旧数据**：继续第 2 步。

### 2. 问语言

不管用户第一句说的是什么，都先用双语问这一句，不加别的：

```
Choose your language / 选择语言：

1. English
2. 中文
3. 自动跟随 / Auto (I'll reply in whatever language you use)
```

### 3. 根据回答设定

| 用户选 | display_language | storage_language |
|---|---|---|
| 1 / English | `en` | `en` |
| 2 / 中文 | `zh` | `zh` |
| 3 / 自动 / Auto | `auto` | 用户回答这一句时用的语言。只回了数字、看不出来时，再问一句"存储用中文还是英文？Store data in Chinese or English?" |

只有旧数据的情况：存储语言已经定了，这里只设 `display_language`。

### 4. 建立数据文件

1. 从 `.agents/templates/<storage_language>/` 读出每个模板文件，原样写到根目录。用读写工具完成，不要依赖 `cp` 这类系统命令，这样任何电脑都能运行。
2. 例外：`learning-skill.md` 和 `project.md` 是档案样板，留在模板文件夹里，不要复制到根目录。
3. 在根目录建空的 `journal/`、`learning/`、`projects/` 文件夹（各写一个 `.gitkeep` 空文件即可）。
4. 根目录没有 `state.md` 的话，新建一个，内容如下：
   ```
   # 系统状态 State

   由助理维护，不用手动改。Maintained by the assistant. No need to edit.

   上次检查日期 last_check: none
   上次周回顾 last_review: none
   上次提醒周回顾 last_review_nudge: none
   ```
5. 根目录已经存在的同名文件不要覆盖。
6. 改写 `config.md` 里的两项语言设置。

### 5. 收尾

用选定的语言回复。中文：

```
好了，以后用中文。
```

英文：

```
All set. I'll use English from now on.
```

然后接着 AGENTS.md 的开场流程：查时间、顺延检查，再回一段招呼。如果用户最开始那句话是具体内容，现在处理它。

## 情况二：切换显示语言

用户说"以后说英文"、"switch to Chinese"、"自动跟随"这类话：
1. 只改 `display_language`。
2. 存储语言不动，数据文件不动。
3. 用新语言回一句确认。

## 情况三：转换存储语言

用户明确说"把数据转成英文"、"convert my data to Chinese"这类话时才做。只是切换显示语言，不要触发这个。

### 先确认

```
这会把所有数据文件的字段改成英文写法。你写的任务名称、点子、感想保持原样，不翻译。
确定要转吗？
```

### 转换

按 AGENTS.md 的对照表，逐个改写这些文件：
- `tasks.md`、`goals.md`、`goals-archive.md`、`ideas.md`、`experiences.md`、`habits.md`
- `journal/` 下所有文件
- `learning/` 和 `projects/` 下所有档案。文件名是我起的名字，属于原话，不改名。

规则：
- 只换字段名、字段值、分组标题、journal 的日期标题和标记。
- 用户的原话一律不动。
- 文件开头的说明注释，换成目标语言模板里的版本。
- 一个文件改完再改下一个。中途出错就停下，告诉用户哪个文件改到一半。

### 收尾

1. 改 `storage_language`。
2. 回一句："转好了，共改了 N 个文件。"
