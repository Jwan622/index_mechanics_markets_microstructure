# Lesson 11: Official Index Methodology Documents

## Learning Goal

Lessons 9, 9a, and 10 used specific rules from S&P and FTSE Russell: a $22.7bn size threshold, a ±2.5-point band, a $150 million test for share offerings. This lesson is about the skill behind those lessons: picking up *any* index methodology document, finding the sentences that create trades, and turning them into a forecast of who must buy or sell, how much, and when.

The key idea is that methodology documents contain different kinds of sentences, and each kind creates a different trading problem. A hard numeric rule can be computed. A discretion clause can only be given a probability. A timing clause sets the date the flow arrives. An exception or a buffer decides who is exempt. Reading a methodology document well means sorting its sentences into these kinds.

## What a Methodology Document Is

A methodology document is the index provider's official rulebook. It is versioned and dated, and it changes. It is rarely a single file. A main document points to supporting documents, and the detail you need is often in one of those.

Here is the chain for the two families used so far, with the versions read for these lessons:

| Provider | Document | Version | What it covers |
|---|---|---|---|
| S&P | U.S. Indices Methodology | Jul 2026 | Eligibility, selection, timing |
| S&P | Index Mathematics | Sep 2026 | Divisor, total return math |
| S&P | Policies & Practices | Aug 2026 | Corporate actions, share updates |
| S&P | Float Adjustment | — | How IWFs are set |
| Russell | Construction and Methodology | v7.2, Aug 2026 | Eligibility, ranking, bands, schedule |
| Russell | Free Float Restrictions | — | How float is measured |

Lesson 10's spin-off rule (add at a price of zero, delete later) isn't in the S&P U.S. Indices Methodology at all. It is in Policies & Practices. A reader who stops at the main document misses it.

## The Seven Questions to Answer

Whatever the provider, a flows reader needs the same seven answers. This table shows where each one lives in the two documents already studied:

| Question | S&P | Russell |
|---|---|---|
| Who is eligible? | Eligibility Criteria | §5 |
| How is size measured and cut? | Market Capitalization | §6 |
| How is float measured? | Float Adjustment Methodology | §7 + Free Float doc |
| Who decides? | Index Committee section | §2, §4 (rules only) |
| When is the review, announcement, and effective date? | Timing of Changes | Appendix F |
| What protects current members? | "Not for continued membership" | §6.10 bands |
| How are corporate actions handled? | Policies & Practices | §9 |

Fill in all seven before estimating any flow. A missing answer usually becomes a wrong trade.

## Four Kinds of Sentences

Every sentence that matters for flow falls into one of four kinds. Each kind needs a different response from a desk. The examples are paraphrased from the S&P and Russell documents.

| Kind | Example | What the desk does |
|---|---|---|
| Hard rule | Russell: close at or above $1.00 on rank day | Compute it |
| Discretion | S&P: the committee selects constituents | Estimate a probability |
| Timing | S&P: at least 3 business days' notice of adds | Mark the trade date |
| Exception | Russell: current members can use a 30-day average price | Check who is exempt |

**Hard rules** are numbers or yes/no tests that anyone can run with the right data. They make flow *computable*. Lesson 9a ran Russell's rules on four companies with no judgment involved.

**Discretion clauses** use words such as "at the discretion of the Index Committee" or "in the sole judgment of." They mark where the rulebook stops and people decide. Flow behind a discretion clause can only be forecast as a probability, as in Lesson 9's discussion of predicting the S&P committee.

**Timing clauses** say when things are measured, announced, and implemented. They don't change *how much* trades, but they decide *when*, and therefore who can position ahead of it.

**Exceptions** carve out specific cases: current members, promotions from a sister index, very large events. They're often in footnotes, and they often reverse what the main rule seems to say.

## Exceptions Change the Answer: Three Share Offerings

Lesson 10 showed that a share issuance makes index funds buy, and that S&P's rule for *when* depends on the offering's size. Here the full clause is read carefully, including an exception that is easy to miss.

The S&P Policies & Practices document says a public offering gets **accelerated implementation** (applied within days, with one business day's notice for US stocks) if it is at least $150 million **and** at least 5% of the shares before the offering. Otherwise it waits for the quarterly share update. Then a separate paragraph adds an exception: events of **at least $1 billion** are accelerated *even if they are below the 5% threshold*.

Written out as a decision, checked from the top down:

| Check | If yes |
|---|---|
| 1. Offering ≥ $1bn? | accelerated |
| 2. Offering ≥ $150m **and** ≥ 5% of shares? | accelerated |
| 3. Neither | next quarterly update (third Friday of Mar, Jun, Sep, Dec) |

Now apply it. Harbor Corp is an S&P 500 member with 400m shares at $75 (a $30bn company) and a float factor of 1.00. Three possible offerings of new shares:

**Step 1. Size each offering in dollars and as a share of the existing shares.**

| Offering | Dollars | Share of 400m |
|---|---:|---:|
| 30m shares | 30m × $75 = $2.25bn | 7.5% |
| 16m shares | 16m × $75 = $1.2bn | 4.0% |
| 10m shares | 10m × $75 = $0.75bn | 2.5% |

**Step 2. Run the decision.**

| Offering | ≥ $1bn? | ≥ $150m and ≥ 5%? | Timing |
|---|---|---|---|
| 30m shares | yes | yes | accelerated |
| 16m shares | **yes** | no (4.0%) | **accelerated** (exception) |
| 10m shares | no | no (2.5%) | quarterly update |

The 16m-share offering is the case that catches people. It fails the 5% test, so reading only the first rule says "quarterly." The $1 billion exception overrides that.

**Step 3. Size the index flow.** Lesson 9 showed that index trackers own the same slice of every member's tradable shares. Suppose, for illustration, that trackers own **20%** of every S&P 500 member's float. That is a stylized round number; Lesson 14 estimates the real one. New tradable shares × 20% = shares that trackers must buy:

| Offering | Trackers buy | At $75 | When |
|---|---:|---:|---|
| 30m shares | 20% × 30m = 6.0m | $450m | within days |
| 16m shares | 20% × 16m = 3.2m | $240m | within days |
| 10m shares | 20% × 10m = 2.0m | $150m | next quarterly date |

The size of the flow follows directly from the offering size. The *date* comes from reading the timing clause and its exception. A desk that missed the $1 billion exception would expect the 16m-share flow weeks later than it actually arrives.

## Buffers: Why Rulebooks Protect Current Members

Most methodology documents contain a **buffer**: a rule that treats current members more leniently than newcomers. Lesson 9a covered two examples. Russell has a ±2.5-point band at the 1,000th-company cutoff, and S&P applies its entry criteria to new entrants only. Here is the general idea and why it exists.

### The problem: churn at the boundary

Take a company, Juniper, that sits right at the edge of a size cutoff at rank 1,000. It is in the large-cap index going into review 1, and over six reviews its rank wobbles around the cutoff.

**With a hard cutoff**, Juniper is large-cap whenever its rank is 1,000 or better, and small-cap otherwise.

**With a buffer**, a current member only moves if it goes clearly past the cutoff. To keep the arithmetic simple, use a band of ±25 ranks (975 to 1,025). This is a simplified stand-in for Russell's band, which is measured in cumulative percentile, not ranks. Juniper stays large-cap unless its rank is worse than 1,025.

| Review | Rank | Hard cutoff | Buffer (±25) |
|---:|---:|---|---|
| 1 | 990 | large | large |
| 2 | 1,010 | small (moved) | large |
| 3 | 995 | large (moved) | large |
| 4 | 1,008 | small (moved) | large |
| 5 | 997 | large (moved) | large |
| 6 | 1,004 | small (moved) | large |

Count the moves. The hard cutoff makes Juniper migrate **five times** in six reviews. The buffer makes it migrate **zero** times, because every rank from 990 to 1,010 is inside 975–1,025.

Lesson 9's company Z showed what each migration costs: moving up meant net passive *selling* of about 8% of the float, and moving down meant net buying. Under a hard cutoff, Juniper would be pushed back and forth through that trade five times, though its size barely changed.

### The cost of a buffer

A buffer isn't free. It makes the index a slightly less exact picture of the market. Lesson 9a's real 2025 data showed the result: the largest Russell 2000 company ($7.4bn) was more than three times the size of the smallest Russell 1000 company ($2.0bn). Every rulebook picks a point between two goals:

| Goal | Hard cutoff | Wide buffer |
|---|---|---|
| Index matches the market exactly | better | worse |
| Low turnover for index funds | worse | better |

For a desk, buffers have one big consequence: **membership depends on history.** To predict who moves, you need each company's current index as well as its new rank or size. The technical name for a system whose output depends on its past state is *hysteresis*.

### Other families do the same thing in different ways

MSCI and CRSP, two other large index providers, also build in buffers. Their methods differ from Russell's.

**MSCI** sets its size cutoffs in each market to cover a target share of market value: 70% for large-cap, 85% for standard (large plus mid), and 99% for its broadest index, the IMI (Investable Market Index: large, mid, and small). It reviews these semi-annually, in May and November. MSCI researchers describe "multiple buffers" that limit inclusions, exclusions, and migrations between size segments, so a company can keep its segment while sitting in a zone just below the cutoff.

**CRSP**, whose indexes Vanguard uses for several funds, says it reduces turnover in three ways: buffers around its breakpoints, "packeting," which it describes as cutting each migration event in half, and spreading changes over five trading days. (CRSP was acquired by Morningstar in 2026, and its indexes are being renamed Morningstar Market Indexes.) The exact packeting mechanics are in CRSP's methodology guide, which wasn't read for this lesson, so the details aren't covered here.

The general lesson: every major provider has a turnover-control clause. Find it before predicting any migration.

## What Is Announced, and What Must Be Inferred

The final reading task is to sort every piece of information into "the provider publishes this" or "you must work it out yourself." The gap between the two is where desks compete.

| Item | S&P 500 | Russell |
|---|---|---|
| Membership changes | Announced at least 3 business days ahead; before that, only probabilities | Computable after rank day; official preliminary list 4–5 weeks before effective |
| Share count changes | Large offerings: 1 business day's notice; others at quarterly update | At reconstitution and quarterly updates |
| Float changes | Annual review, plus large events | Full review in June; material changes in December |
| Effective time | After the close on the stated date | After the close on reconstitution day |

Read the table like this. For **Russell additions**, the information is effectively public once rank day closes, because the rules are mechanical. The edge goes to whoever computes the list fastest and most accurately, including the band. For **S&P additions**, the information doesn't exist until the committee decides, so the edge goes to better probability estimates and fast reactions to announcements. For **share changes**, both providers apply public filings with a delay, so a desk that reads the offering documents can forecast the index change before it is announced.

## From a Fund to Its Index

A methodology document only matters if money tracks the index. The link is in each fund's prospectus, which names the index the fund follows. For example, iShares' IWM tracks the Russell 2000, and the large S&P 500 ETFs (such as IVV and VOO) track the S&P 500. Several Vanguard funds track CRSP indexes. The money tracking an index, spread across all the funds and accounts that copy it, is what turns a rule into a flow. Lesson 14 is about adding it up.

## Keeping Up with Changes

Rulebooks change, sometimes in ways that move a lot of money. Three examples from these lessons:

| Change | Effect |
|---|---|
| Russell went from annual (June) to semi-annual (June and December) rebuilds from December 2026 | A second reconstitution trade each year |
| S&P stopped excluding new multiple-share-class companies | Companies such as Granite in Lesson 9a became possible candidates |
| S&P's size threshold is reviewed every quarter | The $22.7bn bar moves with the market |

Providers announce these through **index notices** and, for bigger changes, **consultations**, where they publish a proposal and invite comment before deciding. Check the version date on any document you rely on, and watch the provider's notices page.

## Common Misconceptions

**"The main methodology document has everything."** Key rules often sit in supporting documents. S&P's spin-off treatment and share-offering thresholds are in Policies & Practices, not in the U.S. Indices Methodology.

**"Public rules mean predictable flow."** Only the hard-rule parts are computable. Discretion clauses, such as the S&P committee's choices, still need probabilities.

**"If a company fails a rule, it leaves the index."** Many rules apply only to new entrants. S&P says so explicitly, and Russell's band protects current members near the cutoff. Check whether a rule applies to members, to newcomers, or to both.

**"Buffers are a technicality."** A buffer decides whether a company triggers a large migration trade or none at all. Juniper would have faced five forced trades without one, and zero with one.

**"The timing clause doesn't matter if you know the size."** The same $240m of buying arrives within days or at the next quarterly date depending on a $1 billion exception. Who can position ahead of the flow depends on the date.

## Recap

A methodology document is a versioned rulebook, usually spread across a main document and several supporting documents. Reading it for flows means answering seven questions: eligibility, size, float, who decides, timing, protection of current members, and corporate actions. It also means sorting sentences into four kinds. Hard rules can be computed, discretion clauses need probabilities, timing clauses set the trade date, and exceptions decide who is exempt. The S&P share-offering rule shows why exceptions matter. A 4% offering looks like a quarterly event under the main rule, but the $1 billion exception makes it an accelerated one. Buffers protect current members to reduce turnover, at the cost of a less exact index, and they make membership depend on history. The gap between what providers announce and what readers can work out for themselves is where desks compete. For Russell, that is fast, accurate computation. For S&P, it is probability and speed of reaction.

## New Terms

**supporting document**: A separate document referenced by a main methodology, holding detailed rules such as corporate-action treatment or float calculation.

**hard rule**: A numeric or yes/no criterion that anyone with the data can apply.

**discretion clause**: Language that leaves a decision to the provider's committee or judgment, so the outcome can only be estimated.

**timing clause**: A rule that sets when data is measured, when changes are announced, and when they take effect.

**exception**: A rule that exempts specific cases from a general rule, often in a footnote or separate paragraph.

**buffer**: Any rule that treats current members more leniently than newcomers, in order to reduce turnover.

**turnover**: The share of an index's value that changes at a review. High turnover means more forced trading for funds.

**hysteresis**: The property that a system's current state depends on its history. In indexes, membership depends on where a company was before, not only on its current size.

**packeting**: CRSP's term for a turnover-reduction technique that, by its own description, cuts each migration event in half.

**index notice / consultation**: The provider's official announcement of a rule change, or a published proposal inviting comment before a change is made.

## Questions to Test Yourself

1. An S&P 500 member sells new shares equal to 3% of its share count, raising $1.4bn. Is the change accelerated or quarterly?

Accelerated. It fails the 5% test, but S&P accelerates any event of at least $1 billion regardless of the 5% threshold.

2. Why must a desk know current index membership, not just the new ranking, to forecast migrations?

Buffers let current members stay put inside a zone where a newcomer would be placed by rank alone. Two companies of the same size can end up in different indexes depending on where they started.

3. A methodology sentence says "constituent selection is at the discretion of the Index Committee." What kind of sentence is it, and how should a desk treat the resulting flow?

It is a discretion clause. The flow can't be computed until the announcement, so the desk works with probabilities and prepares to react quickly when changes are announced.

4. What does a buffer gain, and what does it give up?

It cuts turnover and forced trading for index funds near a cutoff. In exchange, the index stops being an exact picture of the market, so a "small-cap" index can contain companies larger than some "large-cap" members.

5. Where would you look in S&P's documents to learn how a spin-off is treated, and what would you find?

In the Equity Indices Policies & Practices document, not the main U.S. Indices Methodology. It says the spin-off is added at a price of zero with no divisor change, then removed after at least one day if it isn't eligible, which creates forced selling.

## Sources

S&P Dow Jones Indices. "S&P U.S. Indices Methodology." July 2026. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)

S&P Dow Jones Indices. "Equity Indices Policies & Practices Methodology." August 2026. Material Share/IWF Changes (Accelerated Implementation Rule) and Announcement Policy. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf)

S&P Dow Jones Indices. "Index Mathematics Methodology." September 2026. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf)

FTSE Russell. "Russell US Equity Indexes: Construction and Methodology." v7.2, August 2026. [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf)

FTSE Russell. "2025 Russell Reconstitution Recap." [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf)

Gupta, Abhishek, Pavlo Taranenko, and Sebastien Lieblich. "Index Rebalancing During High Volatility: A Balancing Act." MSCI, May 13, 2020. [https://www.msci.com/research-and-insights/blog-post/index-rebalancing-during-high-volatility-a-balancing-act](https://www.msci.com/research-and-insights/blog-post/index-rebalancing-during-high-volatility-a-balancing-act)

CRSP. "Key Concepts" and "CRSP Market Indexes Methodology." [https://www.crsp.org/indexes/key-concepts/3/](https://www.crsp.org/indexes/key-concepts/3/) and [https://www.crsp.org/indexes/crsp-market-indexes-methodology/](https://www.crsp.org/indexes/crsp-market-indexes-methodology/)
