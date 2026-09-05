---
name: write-next-lesson
description: Writes the next curriculum lesson file for this repo. Use when the user asks to write the next lesson, generate lesson N, continue the curriculum, or invokes /write-next-lesson.
disable-model-invocation: true
icon: book-open
color: blue
---

# Write Next Lesson

Write exactly one new lesson file. Then stop.

Do not copy `AGENTS.md` or `CURRICULUM.md` into the reply. Read them and follow them.

## Workflow

1. List existing `lesson_*.md` files at the repo root.
2. Read `CURRICULUM.md` and find the first curriculum part whose filename does not exist yet.
3. Read `AGENTS.md` for teaching style and required lesson structure.
4. Read the immediately previous lesson so the new one continues it and does not repeat or steal a later part.
5. If the user named a specific lesson, write that file only if it is the next missing one, or they explicitly asked to skip ahead. Otherwise tell them which file is next and wait.
6. Read `SOURCES.md`. Search the markets list first (Jane Street, Optiver, papers, exchange/FINRA/SEC docs). Cite the specific page. Do not invent facts, numbers, or citations.
6a. sites to use in addition to any others you find useful: https://www.uber.com/us/en/blog/engineering/data/, https://blog.janestreet.com/, https://www.startdataengineering.com/, https://www.theseattledataguy.com/data-science-consulting-blog/#page-content, https://netflixtechblog.com/all?topic=data-engineering, https://blog.cloudflare.com/. you can use those to cite ideas for data engineering. 
7. Write one file at the repo root using the curriculum filename.
8. Stop. Do not write the following lesson. Do not commit unless asked.

## File and structure

Filename: `lesson_x_<short_lowercase_title>.md`

Required sections:

1. One `#` title
2. `## Learning Goal` near the top
3. Middle sections that actually teach the topic
4. `## Recap` in paragraph form
5. `## New Terms` with short plain-English definitions
6. `## Questions to Test Yourself` — four mechanism questions, each with a two-sentence answer

Connect the lesson to participants, incentives, timing, liquidity, risk transfer, and price impact.

## Style

Follow `AGENTS.md`. No "By the end of this lesson", "Let's dive in", or "It is important to note." One small numbered example. Define jargon before using it. Include at least one common misconception.

## Do not

- Generate more than one lesson
- Skip a missing earlier lesson unless the user explicitly said to
- Dump the whole curriculum into the chat
- Repeat the previous lesson's content
- Leave uncited empirical claims
