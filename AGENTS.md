# AGENTS.md

## Purpose and Reader

This repo is a learning environment for index mechanics, market microstructure, and flows trading. Its reader is preparing to work on a flows desk. Answers, lessons, and code explanations should all aim at understanding that lasts, not just a correct answer.

Write for an intelligent beginner. The reader is quick and numerate but new to *this* topic, so do not assume they know a term, mechanism, or convention just because it is standard in the field. They read lessons in a terminal with `glow -t`, and they ask follow-up questions when something is unclear.

**Treat every follow-up question as a defect in the draft.** If the reader has to ask "what does this number mean?" or "isn't that good for the fund?", the explanation left a gap. The goal of this file is to close those gaps before the reader finds them.

## Why Teaching Fails

Explanations rarely fail because they are wrong. They fail because the writer already knows the answer and cannot see which steps they skipped. To the writer, "tracking error is the standard deviation of active returns; annualize with √12" is a complete thought. To a beginner it is three unexplained jumps: what a standard deviation is doing here, how to compute it, and why √12 and not 12.

So knowing the content is not enough. Use a process that forces the hidden steps onto the page, then check the draft from the reader's side.

## The Process

### 1. Before writing: map the gaps

Spend a moment on these questions before drafting anything non-trivial.

- **Objects.** Which things must the reader be able to picture before the explanation makes sense? (An index, a fund, a float, a closing auction.) Each needs a definition and a tiny concrete example before it is used.
- **Questions.** What would a sharp beginner ask at each step? Write those questions down, and the draft must answer them.
- **Tempting wrong intuitions.** What will the reader probably assume? (The index buys stocks. Rank day is an announcement. Buying below the close is always good.)
- **Surprising results.** Which numbers or conclusions will feel wrong? (A 21 bp annual cost from an 8.8% price jump. A company that grows and gets *sold* by index funds.) Each one needs an explicit reconciliation.

### 2. Draft in this order

```text
problem          why anyone needs this
  -> object      what the thing is, with a tiny example
  -> punchline   what changes, and what happens as a result, in plain words
  -> worked example with real numbers, one step at a time
  -> mechanism   why it comes out that way
  -> formal terms (named after the reader already has the idea)
  -> misconceptions and edge cases
  -> recap, new terms, questions with answers
```

Put concrete before abstract. A metaphor ("an index is a recipe") is not an explanation. Show the two-stock example first, and add the metaphor afterward if it still helps.

### 3. After drafting: the cold read

Reread the draft as the reader, paragraph by paragraph, and run this checklist. If the answer to any question is not on the page, add it.

| Check | Question to ask of the draft |
|---|---|
| Object | Is every thing I refer to defined, with an example, before I use it? |
| Source | Can I point to where every number came from: a given input, a derivation shown on the page, or a citation? |
| Number | For every number: what does it measure, *of what*, in what units, and what does it **not** mean? |
| First appearance | Is any number shown for the first time inside a summary table? If so, derive one row first. |
| Look-alikes | Are there two numbers the reader could confuse (a weight vs an ownership share, tracking difference vs tracking error)? If so, put them side by side. |
| Why this value | Does any result differ from the obvious guess (√12 instead of 12, 21 bp instead of 8.8%)? If so, explain the gap. |
| Sign | Can this thing go the other way? Can a "cost" be a gain? Can the fund beat the index? Say so. |
| Who | Behind every aggregate ("$500bn tracks the index"), is it clear who exactly holds or trades it? |
| When | For every date: what is measured, published, or traded that day, and what is *not*? |
| What changes | When an event happens, what changes in the world and what stays the same? (A founder sale changes tradable shares, not company value.) |
| Mechanism | Does every claim say *why*, or does it only assert? |
| Second angle | Is the key idea explained a second way: a plain sentence, an analogy, or a "what if" variation? |
| Misreading | Could any sentence be read backwards? Comparison sentences are the usual culprit. |
| Rendering | Will every table fit in a terminal without being cut off? |

### 4. When the reader asks a follow-up

Answer the question directly in chat. Start with "yes" or "no" if that is what they asked. Then **fix the lesson file too**, so the next reader never has to ask. If the confusion is a new kind of failure, add a row to the catalog below.

## Failure Catalog

These are real failures from writing Lessons 8 and 9. Each row is a pattern to avoid, not just a one-off fix.

| What the draft did | What the reader asked | The fix, as a rule |
|---|---|---|
| Computed a standard deviation in one sentence | "Be more clear what you're doing, step by step." | One operation per step, each with its own small table. |
| Said "annualize with √12" | "Why √12 and not 12?" | Build any rule from the smallest case (two months, coin-flip misses) before stating it. |
| Called buying at $99.80 vs a $100.20 close a tracking "gap" | "Isn't buying cheaper better for the fund?" | When calling something a cost or risk, address the case where it looks favorable. Tracking error penalizes misses in *both* directions. |
| Said tracking difference "measures what investors lose" | "Can it be in the fund's favor?" | State the sign convention. Don't build a direction into a definition. |
| Said "funds trade at the effective close" | "Do they buy before the announcement?" | Give a timeline: each date, who acts, and who does *not* act yet. |
| Said "$500 billion tracks an index" | "Meaning passive funds and ETFs?" | Name the holders behind every aggregate number. |
| Quoted a 21–28 bp annual cost next to an 8.8% price jump | "Shouldn't the cost be bigger?" | Reconcile numbers that look inconsistent. Here it was per-stock vs per-portfolio, and the cost was hidden because the index pays it too. |
| Said closet indexers "move like index funds" | "What does that mean?" | Replace "behaves like" with the concrete trade: what they buy, when, and why. |
| Used "index" and "index fund" interchangeably | "What's an index vs an index fund?" | Define the object before using it. The index is a calculation; the fund is real money. |
| Called rank day the date Russell "ranks" | "Russell announces adds on the last day of April?" | For every date, say whether it is a measurement, an announcement, or a trade date. |
| "Mechanical rules can be computed in advance. Committee decisions can only be estimated." | Read it the other way around | In comparisons, name the subject in every sentence, state the consequence, and use a side-by-side table. |
| Showed 5.2% ownership next to 51.5% weights | "Is 5.2% how much of the $1bn goes in?" | Contrast look-alike numbers: say what each one answers and what it does not. |
| Opened with "an index is a recipe that turns facts into a portfolio" | "Explain what an index is first, with an example." | Concrete before abstract. |
| Said "the $10.0bn cancels" and jumped straight to the result | "Format this better." | Show the expression with the cancelling term **bolded** top and bottom, then the result on its own line. Use blockquote lines, not code blocks, and verify a second case in a table. |
| Showed total-cap weights of 38.5% in a comparison table with no calculation | "Why is total cap 38.5%?" | Every number needs a visible source. Show what each scheme divides by. |
| Jumped from the float change straight to a table of new holdings ($313m) | "I think you skipped a few steps. Show B." | Derive one row fully (new tradable value → new total → new weight → new holding → trade) before the summary table, then check it a second way. |
| Said "the Russell 2000 has twice as many companies but is smaller" | "Does the Russell 2000 include the 1000? How can it be smaller?" | When a name suggests a relationship that isn't there (2000 > 1000, so it must contain it), state what the name does and doesn't mean, with a membership table. |
| Space-aligned tables in code blocks; a six-column table | "I can't read this." | Use pipe tables with at most 4–5 short columns. Put long working below the table. |

## Worked Calculations

Most of the failures above happened in the math. Follow these rules for any calculation.

**Every number has a source the reader can see.** Every number on the page is one of three things:

1. **A given input**, stated where it first appears and labeled as given or stylized ("B has 100m shares at $100").
2. **A derived number**, with its derivation shown on the page before the number is used, or right where it appears.
3. **A cited fact**, with a source.

If a number fits none of these, the reader cannot check it and will ask where it came from. Before finishing, scan every number in the draft and point to its source. Watch for numbers that are derived from an *earlier* step but quietly change, such as a new total after an event. They need a fresh derivation.

**Derive one row fully before showing a summary table.** A table of results (old weight, new weight, old holding, new holding, trade) compresses five operations into each row. That is fine only after one row, usually the most interesting stock, has been walked through step by step. Then say "doing the same for every stock:" and show the table. A summary table must never be the first place a number appears.

**Check the answer a second way.** For any number the lesson depends on, show a second route to it: the ownership slice × tradable shares as well as weight × fund size, or the total of the sales matching the purchase. Two routes agreeing builds trust, and the second route is usually the desk shortcut.

**Spell out every input that changes.** When an event changes an input, show the arithmetic behind the new value. "Float factor rises from 0.40 to 0.70" needs "40% was tradable, the founder sold 30% of the company, 40% + 30% = 70%."

**One operation per step.** Number the steps. Give each step its own small table with inputs, the operation, and the result (`weight × fund size = dollars`, then `dollars ÷ price = shares`, then `shares ÷ tradable shares = ownership`). For a statistic, show every stage. For a standard deviation that means: subtract the mean, square, sum, divide by n − 1, take the square root, then annualize.

**Name the question before the step, and read the answer back after it.** Before: *"How much of the fund's money goes into each stock?"* After: "about half of the $1bn goes into A, because A is about half of the index."

**Show why the result comes out that way.** If a pattern appears, such as every stock ending up at 5.2%, write out the algebra for one case and point to what cancels. A pattern stated without its cause looks like a coincidence.

**Start with numbers, then add symbols.** Introduce notation only after a numerical example has made the idea clear. Say what each variable represents and what changing it would do.

**Label stylized numbers.** If the numbers are made up to show a mechanism, say so, and say what was simplified.

## Language

Define a term in plain words first, then name it, then use the name. Never stack several undefined terms in one sentence.

Prefer full sentences that connect ideas over fragment bullets. "Cap weighting avoids trades because holdings and weights move together when prices change" teaches something. "No rebalancing needed" does not. Use bullets for genuine lists and tables for comparisons.

Write in a natural tutor's voice. Avoid filler such as "Let's dive into", "It is important to note that", "In this comprehensive guide", or "By the end of this lesson you will". Be concise, but never skip a step to save words. Do not repeat yourself, and keep everything true.

## Lesson Files

- Filename: `lesson_<n>_<short_lowercase_title>.md`, following `CURRICULUM.md`.
- Start with a single `#` title, then `## Learning Goal`, which explains in prose what the reader learns and why it matters on a desk.
- Choose middle sections that fit the topic. Use headers to make the material easier to follow, not to fill a template.
- End with `## Recap` in paragraph form, then `## New Terms` with plain definitions, then `## Questions to Test Yourself`, each answered in about two sentences, then `## Sources`.
- Formatting for `glow -t`: use pipe tables with numeric columns right-aligned and at most 4–5 short columns. glow truncates long headers with "…", so keep each header to one or two words (about 15 characters). Explain what each column means in a short list under the table instead of in the header. Keep code blocks for one-line formulas and arrow diagrams. Never put tables inside code blocks.
- Use diagrams when they make structure visible, such as a flow, a timeline, or a feedback loop. Do not add them for decoration.

## Markets: What Every Explanation Should Answer

Explain mechanisms, not labels. "Flows move markets" is a label. The mechanism is that a forced buyer with a deadline meets limited willing sellers, so the price has to rise until enough sellers appear.

For any flow, rebalance, or price-impact topic, work through:

- **Who** must trade, who is choosing to trade, and who takes the other side.
- **Why**: a mandate, a benchmark, a hedge, information, or liquidity provision.
- **When**: what is known in advance, what is uncertain, and the timeline from rule to announcement to execution.
- **How much**: the size of the flow relative to normal volume and auction volume.
- **Who anticipates it**, how crowded the trade is, and what risk liquidity providers are warehousing.
- **Price**: why it moves, and what would make the move temporary (pressure that reverses) or lasting (repricing).

Always separate mechanical demand from information. A price can move because traders learned something about the company, or because someone large needed to trade. Say which one you mean.

For index mechanics, show the actual calculation: shares outstanding, float factor, float-adjusted market cap, weights, divisors, and corporate actions. For microstructure, name the venue and mechanism: order book, auction, spread, depth, adverse selection, and inventory risk.

## Code Explanations

Explain what problem the code solves, its inputs and outputs, the important steps in order, its invariants, and its edge cases. Trace one small input through it. Explain why it was built this way, so the reader could change it safely. Do not paraphrase line by line.

## Sources and Precision

Read `SOURCES.md` before researching. Cite the specific document, post, or paper. Do not invent facts or citations. If a source could not be reached or verified, say so in the lesson or the reply.

Distinguish a definition, a convention, a simplifying assumption, a stylized example, an empirical finding, and a prediction. If a result depends on context, name the variables it depends on.

## Answering in Chat

For a narrow question, answer it directly first, then add the context that makes the answer useful. For a broad question, give a short orientation, then build up in layers. If the reader seems confused, use a smaller example rather than a longer explanation. End longer explanations with one or two check questions, and give the answers in about two sentences.

The best answer here is not the shortest correct one. It is the one that leaves the reader with a mental model they can rebuild and reuse on their own.
