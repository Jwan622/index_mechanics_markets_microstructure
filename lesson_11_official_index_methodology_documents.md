# Lesson 11: Reading the Index Rulebooks

## Learning Goal

Lessons 8 to 10 kept leaning on specific rules: a $22.7bn size threshold, a band around the Russell 1000/2000 cutoff, a $150 million test for share offerings. This lesson goes to the rulebooks those rules come from, the official methodology documents for the S&P 500 and the Russell US indexes, and teaches a method for reading any of them.

The skill is turning a sentence in a rulebook into an answer a desk can trade on: is this company eligible, which index does it belong in, and on what date will index funds have to buy or sell? That answer comes before any estimate of how much will trade, and a small clause, such as a voting-rights test, a band, or a $1 billion exception, can decide whether billions of dollars move this week, next quarter, or not at all.

## The Big Picture

**Why read the rulebook at all?** Summaries go stale and skip the details that matter. The S&P and Russell documents were both revised in 2026, and the clauses that move the most money are often footnotes or supporting documents that summaries leave out.

**What makes it hard.** A methodology document mixes four kinds of sentences: hard rules you can compute, discretion clauses you can only estimate, timing clauses that set the trade date, and exceptions that exempt some companies. Read them all the same way and you'll get the trade wrong.

**The method.** Answer seven questions for any index, sort each relevant sentence into one of the four kinds, then apply the rules to a concrete company step by step.

The lesson runs in three parts:

| Part | What it covers |
|---|---|
| The method | the document chain, seven questions, four kinds of sentences |
| The S&P 500 | entry checklist, timing, the committee, share-offering rules |
| Russell | country test, screens, ranking, the band, the rebuild calendar |

It ends with four made-up companies run through both rulebooks, and a one-page comparison.

## Part 1: The Method

### What a methodology document is

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

### The seven questions to answer

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

### Four kinds of sentences

Every sentence that matters for flow falls into one of four kinds. Each kind needs a different response from a desk. The examples are paraphrased from the S&P and Russell documents.

| Kind | Example | What the desk does |
|---|---|---|
| Hard rule | Russell: close at or above $1.00 on rank day | Compute it |
| Discretion | S&P: the committee selects constituents | Estimate a probability |
| Timing | S&P: at least 3 business days' notice of adds | Mark the trade date |
| Exception | Russell: current members can use a 30-day average price | Check who is exempt |

**Hard rules** are numbers or yes/no tests that anyone can run with the right data. They make flow *computable*. Part 4 runs Russell's rules on four companies with no judgment involved.

**Discretion clauses** use words such as "at the discretion of the Index Committee" or "in the sole judgment of." They mark where the rulebook stops and people decide. Flow behind a discretion clause can only be forecast as a probability, as Part 2 shows for the S&P committee.

**Timing clauses** say when things are measured, announced, and implemented. They don't change *how much* trades, but they decide *when*, and therefore who can position ahead of it.

**Exceptions** carve out specific cases: current members, promotions from a sister index, very large events. They're often in footnotes, and they often reverse what the main rule seems to say.

## Part 2: The S&P 500 Rulebook

Lesson 9 introduced the S&P 500 as a committee-run index with published screens. Here are the screens in full, then the timing rules, then the committee itself.

### The entry checklist

Here is the full list of screens from S&P's U.S. Indices Methodology (July 2026 version). A company has to pass **all** of them to become a *candidate*. Passing them doesn't mean it gets added; the committee still chooses.

| Rule | Requirement | Why it matters |
|---|---|---|
| Domicile | US company, filing 10-Ks and 10-Qs | Foreign firms and ADRs can't get in, however big they are |
| Listing | NYSE, Nasdaq, Cboe, NYSE Arca, NYSE American, or Texas Stock Exchange | OTC stocks are excluded |
| Structure | Common stock of a corporation (REITs allowed) | No LPs, MLPs, LLCs, BDCs, ETFs, SPACs, ADRs, or preferred stock |
| Size | Total market cap of **$22.7bn** or more | Set to about the 85th percentile of the US market, reviewed each quarter |
| Float size | Float-adjusted cap at least half the size threshold ($11.35bn) | A big company with a tiny float can still fail |
| Float share | IWF at least 0.10 | At least 10% of shares must be tradable |
| Liquidity | Annual dollar volume ÷ float-adjusted cap of at least 0.75, and 250,000+ shares traded in each of the last 6 months | Index funds must be able to buy it without a huge cost |
| Profitability | Positive GAAP net income in the latest quarter **and** over the last four quarters combined | An unprofitable company can't be added at any size |
| Seasoning | Traded for at least 12 months since its IPO (or de-SPAC) | No fast track into the S&P 500 for new listings |
| Sector balance | Considered when choosing among candidates | Two equal candidates can be decided by which sector is underweight |

Three details change how the flow behaves.

**The rules are for getting in, not for staying in.** The methodology says the criteria "are for addition to an index, not for continued membership." A member that falls below $22.7bn or posts a loss is not removed automatically. This is deliberate, to avoid turnover. So the S&P 500 contains companies that couldn't be added today, and deletions are much harder to predict than additions.

**Promotions skip some tests.** A company moving up from the S&P MidCap 400 only has to meet the size rule. It does not need to pass the profitability, liquidity, or float-size tests again. Promotions are an easier path in, and the MidCap 400's largest members are natural candidates.

**The evaluation date is just before the announcement.** Eligibility is checked at the open of trading two business days before the announcement. A company that drops below the threshold a week before a seat opens can miss its chance.

### When changes happen

| Timing | Event | What it means |
|---|---|---|
| Monthly meetings, but no scheduled reconstitution | **Committee decision** | The committee picks additions from eligible candidates, often to replace a company leaving after an acquisition. S&P's methodology says changes are made "on an as-needed basis." |
| At least 3 business days before the effective date | **Announcement** | S&P publishes the change on its website. The methodology requires at least three business days' notice, and the committee may give less. This is the first time the market knows for sure. |
| After the close on the third Friday of March, June, September, and December | **Quarterly rebalance** | Share counts are updated, and many membership changes are timed to take effect then. Index funds trade in that day's closing auction. |
| Any date | **Off-cycle change** | A merger, acquisition, or bankruptcy can trigger a replacement outside the quarterly schedule. |

### The discretion clause: can the committee be predicted?

Partly. The committee is a group of people, not a hidden algorithm. S&P's methodology says its members are full-time S&P Dow Jones Indices staff who meet monthly. They review candidates for addition, sector composition, and pending corporate actions, and "all Index Committee discussions are confidential." The published criteria screen the candidates, and the members then use judgment. Researchers have looked at how much that judgment matters. Li, Liu, and Wei (2021) find "a nontrivial amount of discretion" in S&P 500 membership. Their most striking result is that firms buying S&P credit ratings seem to have a better chance of being added, while buying Moody's ratings shows no such effect. Sharfman and Deluard (2021) point to discretionary choices with big consequences, such as excluding new dual-class companies from 2017. The current methodology no longer has that exclusion: it includes each listed share class separately. They also argue that Tesla would have qualified years before its 2020 addition under a size-only rule, although the profitability test is part of why it waited.

Discretion does not mean randomness, though. A committee that makes many similar decisions leaves a pattern, and that pattern can be learned. This is a natural machine-learning problem: a classifier estimates the probability that each candidate is added next quarter. Agrawal and coauthors (2024) train a random forest on quarterly financial, market, industry, and governance data and report a test F1 score of 0.85. F1 combines how many predicted adds were right with how many real adds were caught. Useful features follow directly from how the committee works:

| Feature | Why |
|---|---|
| Size relative to the smallest current members | A candidate has to look like it belongs |
| Positive earnings, liquidity, float | Published eligibility screens |
| Sector weight in the index vs the market | The committee considers sector balance |
| Being a large member of the S&P MidCap 400 | Many additions are promotions from the MidCap |
| Seats opening (members being acquired) | Additions often happen only when someone leaves |

Three things limit how far a model can go. First, the model can rank candidates, but *timing* depends on when a seat opens, which usually comes from an unrelated merger. Second, there are only a few additions each quarter, so even a good model has to pick from a handful of close candidates, and the evaluation must use a time-based split with data as it was known at the time (Lessons 24–26). Third, everyone can build the same model. Greenwood and Sammon (2025) show that the average S&P 500 addition effect fell from about 7.4% in the 1990s to under 1% in the last decade. Two reasons they give are that changes are more anticipated and that more additions are MidCap promotions, where the buying and selling partly offset. A good forecast is now partly priced in, so the edge comes from being better calibrated or faster than the crowd, not from forecasting at all. Lesson 15 builds a rules-based version of this, and Lesson 25 adds the machine learning.

### A timing clause with an exception: three share offerings

Lesson 10 showed that a share issuance makes index funds buy, and that S&P's rule for *when* depends on the offering's size. Here the full clause is read carefully, including an exception that is easy to miss.

The S&P Policies & Practices document says a public offering gets **accelerated implementation** (applied soon after S&P confirms the offering is complete, with at least one business day's notice for US stocks) if it is at least $150 million **and** at least 5% of the shares before the offering. Otherwise it waits for the quarterly share update. Then a separate paragraph adds an exception: events of **at least $1 billion** are accelerated *even if they are below the 5% threshold*. (In every case the offering must also be underwritten, have a public prospectus, and be confirmed as completed. Lesson 10 lists these conditions.)

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
| 30m shares | 20% × 30m = 6.0m | $450m | soon after the offering |
| 16m shares | 20% × 16m = 3.2m | $240m | soon after the offering |
| 10m shares | 20% × 10m = 2.0m | $150m | next quarterly date |

The size of the flow follows directly from the offering size. The *date* comes from reading the timing clause and its exception. A desk that missed the $1 billion exception would expect the 16m-share flow weeks later than it actually arrives.

## Part 3: The Russell Rulebook

The Russell rules run as a fixed sequence of steps, with no committee. Lesson 9's "What the Russell names mean" covered which ranks belong to which index. This part goes through the steps that produce those ranks.

### Step 1: Is it a US company?

The Russell US indexes only hold companies that FTSE Russell assigns to the US. That sounds obvious, but many companies are incorporated in one country, headquartered in another, and listed in a third. The rulebook settles this with three **home country indicators (HCIs)**:

1. the country where the company is incorporated,
2. the country of its headquarters, and
3. the country where its stock trades most (by two-year average daily dollar volume).

The test runs in order and stops at the first "yes":

| Step | Question | If yes |
|---|---|---|
| 1 | Do all three HCIs point to one country? | That country |
| 2 | Are most of its assets in one of the HCI countries? | The asset country |
| 3 | Is most of its revenue in one of the HCI countries? | The revenue country |
| 4 | Is the headquarters in a country that isn't a tax haven? | The HQ country |

If step 4 fails too, the company is assigned to the country of its main exchange. A company that doesn't trade on an eligible US exchange is never eligible. The rulebook's term for a tax haven here is a "benefit-driven incorporation" country, meaning a place companies incorporate for tax or legal advantages.

**Example 1.** A company is incorporated in Delaware, headquartered in Texas, and listed only on Nasdaq. All three HCIs say "US," so Step 1 assigns it to the US.

**Example 2.** A company is incorporated in the Cayman Islands, headquartered in California, and listed only on the NYSE. The HCIs disagree (Cayman, US, US), so Step 1 fails. Most of its assets are in the US, which is one of its HCI countries, so Step 2 assigns it to the US.

The point for a desk is that country assignment is a rule, not a judgment. A company that redomiciles or moves its headquarters can enter or leave the Russell indexes without changing size at all.

### Step 2: The eligibility screens

A US company must then pass every screen below. Each is checked on **rank day**, the measurement date (last business day of April for the June rebuild, last business day of October for the December rebuild).

| Screen | Rule | Section |
|---|---|---|
| Price | Close at or above $1.00 on rank day | 5.8 |
| Size | Total market cap of at least $30 million | 5.9 |
| Float | At least 5% of shares available to the public | 5.10 |
| Voting rights | At least 5% of all votes held by the public | 5.15 |
| Listing | Trades on an eligible US exchange (not OTC) | 5.6 |
| Structure | Not a SPAC, LP, LLC, BDC, ETF, royalty trust, etc. | 5.11 |
| Share type | Not preferred stock, warrants, rights, or depositary receipts | 5.13 |

Two of these rules treat current members and newcomers differently, and both are easy to miss.

**The $1 price rule.** A newcomer must close at or above $1.00 on rank day, full stop. A current member that closes below $1.00 still passes if its average closing price over the 30 days before rank day was at least $1.00. The rulebook's stated aim is to avoid unnecessary turnover.

**The voting-rights rule.** The 5% voting test was added in 2017 for new companies. Existing members were grandfathered, and since the 2023 reconstitution every company below 5% has been removed. This test is about *votes*, not shares, so it catches companies with super-voting share classes. Case B below works through it.

### Step 3: Rank and cut

Every eligible company is ranked by **total market cap** (all shares × the rank-day closing price, before float adjustment). The largest 4,000 form the broadest index, the Russell 3000E, and every other index is a slice of that list:

| Index | Ranks included |
|---|---|
| Russell 1000 | 1 – 1,000 |
| Russell 2000 | 1,001 – 3,000 |
| Russell 3000 | 1 – 3,000 |
| Russell Midcap | 201 – 1,000 |
| Russell Microcap | 2,001 – 4,000 |

Lesson 9's section "What the Russell names mean" has the full list, including the Russell 3000E, the Top 200, and the Russell 2500, with a picture of how they overlap. The key point is that each name counts companies: the Russell 2000 is ranks 1,001–3,000, not 1–2,000.

Members are then *weighted* by float-adjusted market cap, exactly as in Lesson 9's toy index. Ranking uses total cap. Weighting uses float-adjusted cap.

### Step 4: The band around the cutoff

This is the rule people most often get wrong, so it's taken in four pieces: the problem it solves, the rule in dollars, the rule as the rulebook actually measures it, and what it costs.

#### The problem: churn at the boundary

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

#### The rule in dollars

Section 6.10 of the current rulebook (version 7.2, August 2026) places a band around the market-cap breakpoint "to avoid unnecessary turnover at reconstitution." It applies to reconstitution in general, so it covers both the June and December rebuilds.

The rule treats new and current members differently:

- A **new** company goes by the breakpoint alone: above it means Russell 1000, below it means Russell 2000.
- A **current** member stays in its index as long as it is inside the band around the breakpoint. It only moves if it ends up clearly past the line.

Technically the band is measured in *cumulative percentile of market cap* (±2.5 points), which the next section works through step by step. In practice, FTSE Russell translates it into a range of market caps. Its June 2026 article gives the real numbers:

| June 2026 | Total market cap |
|---|---:|
| Breakpoint (new companies) | $5.7bn |
| Bottom of band | $2.7bn |
| Top of band | $9.6bn |

(For comparison, in June 2025 the breakpoint was $4.6bn and the band ran from about $2.0bn to $7.4bn.)

**Applying it.** Here are six made-up companies checked against the June 2026 numbers. Read each row as a question, "is it inside $2.7bn–$9.6bn?", and then apply the rule for new or current members:

| Company | Status | Total cap | Result |
|---|---|---:|---|
| Spruce | current R2000 | $8.0bn | inside band → **stays R2000** |
| Larch | current R2000 | $11.0bn | above band → moves to R1000 |
| Hazel | current R1000 | $3.0bn | inside band → **stays R1000** |
| Rowan | current R1000 | $2.2bn | below band → moves to R2000 |
| Yew | new | $6.0bn | above $5.7bn → enters R1000 |
| Holly | new | $5.0bn | below $5.7bn → enters R2000 |

Look at Spruce and Holly. Spruce is *bigger* ($8.0bn) but stays in the small-cap index, while Holly is *smaller* ($5.0bn) and also lands in the small-cap index. Now compare Spruce with Yew: Spruce is bigger than Yew, yet Yew goes into the Russell 1000 and Spruce doesn't. The difference is only that Spruce is a current member, protected by the band, while Yew is new and judged by the breakpoint alone.

This happens at real scale. FTSE Russell's preliminary June 2026 data showed 97 Russell 2000 members ranked above the breakpoint but kept in the Russell 2000 by the band, and 111 Russell 1000 members ranked below it but kept in the Russell 1000.

Two consequences matter on a desk:

1. **You need the current membership list, not just the ranking.** A ranking alone would put Spruce in the Russell 1000 and Hazel in the Russell 2000. Both would be wrong.
2. **The indexes overlap in size.** In June 2026, a Russell 2000 company could be worth up to $9.6bn while a Russell 1000 company could be worth as little as $2.7bn.

#### How the rulebook measures it: cumulative percentile

The band isn't measured in ranks. It is measured in **cumulative percentile of market cap**, so that idea comes first.

Line up every company from largest to smallest and keep a running total of market cap. A company's cumulative percentile is the running total up to and including that company, divided by the total of all companies. It answers: *what share of the whole market's value sits in companies this big or bigger?*

Here is a five-company market worth $100bn:

| Rank | Company cap | Running total | Cum. pct |
|---:|---:|---:|---:|
| 1 | $50bn | $50bn | 50 / 100 = 50% |
| 2 | $30bn | $80bn | 80 / 100 = 80% |
| 3 | $10bn | $90bn | 90 / 100 = 90% |
| 4 | $6bn | $96bn | 96 / 100 = 96% |
| 5 | $4bn | $100bn | 100 / 100 = 100% |

Read the third row as: "90% of this market's value is in companies at least as big as company 3." A **lower** percentile means a **bigger** company. That direction is the opposite of what people usually expect, so keep it in mind for the next table.

**The rule.**

Section 6.10 of the Russell rulebook sets these bands:

| Breakpoint | Band |
|---|---|
| Stock #1,000 (Russell 1000 / 2000) | ±2.5 percentile points |
| Stock #200 and #500 | ±2.5 percentile points |
| Stock #2,000 | ±0.5 points (±1% for Microcap) |
| Stock #3,000 and #4,000 | none |

The procedure for the Russell 1000/2000 cutoff:

1. Find the cumulative percentile of company #1,000. Call it the breakpoint percentile.
2. Subtract and add 2.5 points to get the band.
3. A **new** company (not currently in the Russell 3000) ignores the band. It goes by rank: 1,000 or better means Russell 1000.
4. A **current** Russell 3000 member inside the band stays in its current index.
5. A current member outside the band goes wherever its rank says.

**A worked example.**

These numbers are stylized, chosen to show the rule. Suppose company #1,000 sits at a cumulative percentile of 90.0%.

> band = 90.0% − 2.5 to 90.0% + 2.5 = **87.5% to 92.5%**

Five companies sit near the cutoff:

| Company | Index now | Rank | Cum. pct |
|---|---|---:|---:|
| Birch | R2000 | 960 | 86.8% |
| Alder | R2000 | 985 | 88.9% |
| Elm | not in R3000 | 990 | 89.2% |
| Cedar | R1000 | 1,020 | 91.2% |
| Dogwood | R1000 | 1,060 | 93.1% |

Take them one at a time.

**Birch.** It is a current member, so check the band. 86.8% is below 87.5%, outside the band on the large side. Birch has grown clearly past the line, so it follows its rank (960) and **moves up to the Russell 1000**.

**Alder.** It is a current member and ranks 985, better than 1,000. A hard cutoff would promote it. But 88.9% is inside the 87.5–92.5% band, so it **stays in the Russell 2000**. Its growth isn't large enough to count yet.

**Elm.** It is not a current Russell 3000 member, so the band doesn't apply. It ranks 990, which is 1,000 or better, so it **enters the Russell 1000**.

**Cedar.** It is a current Russell 1000 member and has slipped to rank 1,020. 91.2% is inside the band, so it **stays in the Russell 1000**.

**Dogwood.** It is a current member at 93.1%, outside the band on the small side. It follows its rank (1,060) and **moves down to the Russell 2000**.

| Company | Hard cutoff says | Band rule says |
|---|---|---|
| Birch | R1000 | R1000 (moves up) |
| Alder | R1000 | **R2000 (stays)** |
| Elm | R1000 | R1000 (new entry) |
| Cedar | R2000 | **R1000 (stays)** |
| Dogwood | R2000 | R2000 (moves down) |

Compare Alder and Elm. Alder ranks 985 and stays in the Russell 2000. Elm ranks *lower*, at 990, and goes into the Russell 1000. The difference is history: Alder is a current member, so the band applies to it, while Elm is new. **You cannot predict Russell membership from the ranking alone. You also need the current membership list.**

The rulebook's own example in Section 6.11 works the same way with real-looking numbers. In it, a current Russell 1000 member just below the $2 billion breakpoint stays in the Russell 1000 because it is inside the band.

#### What the band does in real data

FTSE Russell's recap of the June 2025 reconstitution shows how much overlap the band creates. Both rows are after banding is applied:

| June 2025 | Company | Total cap |
|---|---|---:|
| Smallest Russell 1000 member | Newell Brands | $2.0bn |
| Largest Russell 2000 member | Ensign Group | $7.4bn |

The largest company in the "small-cap" index was more than three times the size of the smallest company in the "large-cap" index. Without banding, that couldn't happen, because every Russell 1000 company would be bigger than every Russell 2000 company. With banding, the boundary between the two indexes is a zone rather than a line, and current members on either side of the zone stay where they are.

**Why is the real band so much wider than the worked example?** In the worked example, the band covered only a few dozen ranks on each side of 1,000: Birch at rank 960 was already outside it, and so was Dogwood at 1,060. In the real market it spans far more, because 2.5 points of *cumulative market cap* is a huge amount of value compared with the size of each company near the cutoff. A rough calculation with the 2025 recap's totals:

**Step 1. Total market value.** The recap gives $55.7tn for the Russell 1000 and $2.7tn for the Russell 2000, so about $58.4tn in all (ignoring the much smaller Microcap).

**Step 2. Value inside 2.5 points.**

> 2.5% × $58.4tn ≈ **$1.46tn**

**Step 3. Number of companies.** Companies near the cutoff are worth a few billion dollars each (between $2.0bn and $7.4bn in the table above). At around $4bn each:

> $1.46tn ÷ $4bn ≈ **365 companies** on each side of the breakpoint

So a current Russell 2000 member can grow well past rank 1,000 and still stay in the Russell 2000. This is a rough estimate, not a published figure, but it shows why the overlap in the table is so large.

#### The cost of a buffer

A buffer isn't free. It makes the index a slightly less exact picture of the market. The real 2025 data above showed the result: the largest Russell 2000 company ($7.4bn) was more than three times the size of the smallest Russell 1000 company ($2.0bn). Every rulebook picks a point between two goals:

| Goal | Hard cutoff | Wide buffer |
|---|---|---|
| Index matches the market exactly | better | worse |
| Low turnover for index funds | worse | better |

For a desk, buffers have one big consequence: **membership depends on history.** To predict who moves, you need each company's current index as well as its new rank or size. The technical name for a system whose output depends on its past state is *hysteresis*.

### Step 5: The rebuild calendar

FTSE Russell calls the rebuild **reconstitution**: every company is re-ranked from scratch, and every index's membership is set again. Since 2026 it happens twice a year. Appendix F of the rulebook sets the rules:

| Stage | June rebuild | December rebuild |
|---|---|---|
| Rank day | last business day of April | last business day of October |
| Preliminary lists | 5 weeks before effective | 4 weeks before effective |
| Query period | 2 weeks after the lists | 2 weeks after the lists |
| Lock-down | final 3 weeks | final 2 weeks |
| Effective | after the close, 4th Friday of June | after the close, 2nd Friday of December |
| What's reviewed | everything | new adds and moves between indexes |

What each stage means:

- **Rank day** is the *measurement*. Prices and shares are recorded at the close, and nothing is published. Russell does **not** announce additions on rank day.
- **Preliminary lists** are the first *announcement* of adds, deletes, and migrations, followed by updated lists.
- **Query period** is when the market can point out data errors.
- **Lock-down**: membership is treated as final.
- **Effective** is the *trade date*: index funds trade in that day's closing auction, and the new index applies from the next open.

**December is a smaller rebuild.** It only handles new additions and moves between the Russell 1000, Russell 2000, and Microcap. Float is updated only for material changes, with a 3% buffer, and existing members' voting rights aren't re-checked. Between rebuilds, the only membership changes are quarterly IPO additions and corporate events such as mergers.

**The 2026 dates.** The June column is FTSE Russell's published schedule. The December column follows from Appendix F (30 October is the last business day of October; 11 December is the second Friday of December; lock-down starts after the two-week query period that follows the 13 November lists), and market commentary (New Street IR, October 2026) reports the same dates:

| Stage | June 2026 | December 2026 |
|---|---|---|
| Rank day | Thu 30 Apr | Fri 30 Oct |
| Preliminary lists | Fri 22 May | Fri 13 Nov |
| List updates | 29 May, 5 Jun, 12 Jun, 18 Jun | not yet published |
| Lock-down begins | Mon 8 Jun | about Mon 30 Nov |
| Effective | Fri 26 Jun | Fri 11 Dec |

So the measurement comes about three weeks before the first list, and the trade comes about two months after the measurement. Check FTSE Russell's official notice for December before trading on the dates.

## Part 4: Both Rulebooks Side by Side

### How each protects current members

Part 2 covered the S&P 500's screens. Two features of the S&P rulebook matter most when you compare it with Russell's.

First, there is **no rank day and no scheduled rebuild**. Changes are made as needed, announced with at least three business days' notice. The committee chooses among eligible candidates.

Second, **the screens apply to getting in, not to staying in**. A current member that fails a screen is not removed automatically. This is the S&P version of a band, and it is much wider than Russell's: a member can shrink far below the $22.7bn entry threshold and remain in the index. The rulebook also excuses MidCap 400 members being promoted to the S&P 500 from the profitability, liquidity, and float-size tests. They only need to meet the size rule.

So both families protect current members, but in different ways:

| | S&P 500 | Russell |
|---|---|---|
| Protection for members | Entry rules don't apply to current members | ±2.5-point band at the cutoff |
| How much protection | Large: removal is a committee choice | Limited: outside the band, you move |
| Effect on flow | Deletions are rare and hard to predict | Migrations are computable from rank and membership |

### Four companies, two rulebooks

Each case lists the given facts, then checks the rules one at a time. All four companies are made up.

#### Case A: Northwind Software (profitable enough?)

Given: a US company listed on Nasdaq, at $60 a share with 500m shares. Float factor 0.85. Last quarter's GAAP net income was +$40m, but the last four quarters summed to −$120m. It has traded for five years and is liquid.

**Step 1. Size.**

> total market cap = $60 × 500m = **$30.0bn**
>
> float-adjusted cap = $30.0bn × 0.85 = **$25.5bn**

| S&P 500 check | Rule | Northwind | Pass? |
|---|---|---|---|
| Size | ≥ $22.7bn total | $30.0bn | yes |
| Float size | ≥ $11.35bn float-adjusted | $25.5bn | yes |
| Float share | IWF ≥ 0.10 | 0.85 | yes |
| Profit, latest quarter | > 0 | +$40m | yes |
| Profit, last 4 quarters | > 0 | −$120m | **no** |

Both profit tests must pass. One failure is enough, so Northwind is **not an S&P 500 candidate**.

| Russell check | Rule | Northwind | Pass? |
|---|---|---|---|
| Price | ≥ $1.00 | $60 | yes |
| Size | ≥ $30m | $30.0bn | yes |
| Float | ≥ 5% | 85% | yes |
| Rank | top 1,000? | $30.0bn is far above the cutoff | yes |

FTSE Russell's 2025 reconstitution recap put the smallest Russell 1000 company at $2.0bn of total market cap after banding, so a $30bn company is far inside the Russell 1000. **Northwind is in the Russell 1000 but not the S&P 500.**

The desk angle: if Northwind's next quarterly report pushes the four-quarter sum above zero, it becomes an S&P 500 candidate overnight. An earnings date can start an index-inclusion trade.

#### Case B: Granite Holdings (super-voting shares)

Given: a US company at $120 a share. It has 200m listed class A shares with one vote each, of which 80% are in public hands. It also has 100m unlisted class B shares held by the founders, each carrying 50 votes. Profitable, liquid, listed for years.

**Russell's voting test (Section 5.15).** The question is: what share of all votes is in public hands?

**Step 1. Votes held by the public.** Only class A trades, and 80% of it is public:

> public votes = 200m × 80% × 1 vote = **160m**

**Step 2. Total votes.** Count every share, listed or not:

> total votes = (200m × 1) + (100m × 50) = 200m + 5,000m = **5,200m**

**Step 3. Divide.**

> public share of votes = 160m / 5,200m = **3.1%**

3.1% is below 5%, so **Granite is not eligible for any Russell US index**, however large it is.

**S&P checks.** The S&P methodology has no voting-rights test. It sizes the company using all share classes, listed or not, and then evaluates each listed class separately.

> total market cap = $120 × (200m + 100m) = **$36.0bn** (at least $22.7bn: passes)
>
> class A float-adjusted cap = $120 × 200m × 0.80 = **$19.2bn** (at least $11.35bn: passes)
>
> class A IWF = 0.80 (at least 0.10: passes)

With profitability, liquidity, and seasoning given as passing, **Granite is an S&P 500 candidate but cannot enter any Russell index.**

This is the reverse of Case A. The two rulebooks disagree in both directions, so a stock's presence in one family tells you little about the other.

#### Case C: Cedar Industries (protected by the band)

Given: Cedar from the banding example, a current Russell 1000 member that ranks 1,020 at a cumulative percentile of 91.2%, with the band at 87.5–92.5%.

| Check | Answer |
|---|---|
| Is Cedar a current Russell 3000 member? | Yes, so the band applies |
| Is 91.2% inside 87.5–92.5%? | Yes |
| Result | Stays in the Russell 1000 |

Now change one fact. Suppose Cedar were a newly eligible company with the same rank and size. The band would not apply, and rank 1,020 would put it in the **Russell 2000**. Same company, same size, different index, depending only on whether it was already a member.

#### Case D: Pebble Bio (the $1 rule)

Given: a current Russell 2000 member that closes at $0.92 on rank day. Its average closing price over the previous 30 days was $1.04.

| Check | Member rule | Pebble | Pass? |
|---|---|---|---|
| Rank-day close | ≥ $1.00, or else... | $0.92 | no |
| 30-day average | ≥ $1.00 | $1.04 | yes |

Because it is a current member, the 30-day average rescues it, and **Pebble stays eligible**. A newcomer closing at $0.92 would simply be ineligible, since the 30-day fallback only applies to current members.

### The comparison table

This is the one-page summary the module set out to build. The S&P column comes from the U.S. Indices Methodology (July 2026) and the Russell column from the Construction and Methodology document (v7.2, August 2026), with section numbers where they apply.

| Topic | S&P 500 | Russell |
|---|---|---|
| Who decides | Index Committee, with discretion | Rules only |
| Country | US domicile per S&P policy | Home country indicators, §5.2–5.5 |
| Size | ≥ $22.7bn total cap | Rank by total cap, §6 |
| Float | IWF ≥ 0.10; float cap ≥ half of size bar | ≥ 5% available, §5.10 |
| Voting rights | No test | ≥ 5% public votes, §5.15 |
| Profitability | Positive GAAP income, latest quarter and four quarters | No test |
| Price | No minimum | ≥ $1.00 on rank day, §5.8 |
| Turnover control | Rules apply only to new entrants | ±2.5-point band at #1,000, §6.10 |
| Timing | As needed; at least 3 business days' notice | June and December rebuilds, App. F |
| Weighting | Float-adjusted cap | Float-adjusted cap, §7 |

To check yourself, rebuild this table from the current versions of both documents without looking at it, then compare. Any row you cannot source to a section is one you don't really know yet.

## Other Families: MSCI and CRSP

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
| S&P stopped excluding new multiple-share-class companies | Companies such as Granite in Part 4 became possible candidates |
| S&P's size threshold is reviewed every quarter | The $22.7bn bar moves with the market |

Providers announce these through **index notices** and, for bigger changes, **consultations**, where they publish a proposal and invite comment before deciding. Check the version date on any document you rely on, and watch the provider's notices page.

## Common Misconceptions

**"A company in the top 1,000 by size is in the Russell 1000."** Only if it is new to the Russell 3000 or outside the band. Alder ranked 985 and stayed in the Russell 2000. Membership depends on rank *and* on the current membership list.

**"Bigger companies always qualify for more indexes."** Granite is a $36bn company that is excluded from every Russell index because of its voting structure, while Northwind is excluded from the S&P 500 because of one bad year of earnings. Size is necessary but not sufficient.

**"A lower cumulative percentile means a smaller company."** It means the opposite. The running total starts from the largest company, so the biggest companies have the lowest percentiles.

**"The December rebuild is a repeat of June."** December only handles additions and size migrations, with lighter float updates and no voting-rights review of existing members. Expect less turnover.

**"If a company fails a rule, it leaves the index."** Many rules apply only to new entrants. S&P says its criteria are for addition, not continued membership, so removal is a committee decision, usually triggered by an acquisition. Russell's band protects current members near the cutoff. Check whether a rule applies to members, to newcomers, or to both.

**"The main methodology document has everything."** Key rules often sit in supporting documents. S&P's spin-off treatment and share-offering thresholds are in Policies & Practices, not in the U.S. Indices Methodology.

**"Public rules mean predictable flow."** Only the hard-rule parts are computable. Discretion clauses, such as the S&P committee's choices, still need probabilities.

**"Buffers are a technicality."** A buffer decides whether a company triggers a large migration trade or none at all. Juniper would have faced five forced trades without one, and zero with one.

**"The timing clause doesn't matter if you know the size."** The same $240m of buying arrives soon after the offering or at the next quarterly date depending on a $1 billion exception. Who can position ahead of the flow depends on the date.

## Recap

A methodology document is a versioned rulebook spread across a main document and supporting documents. Reading one for flows means answering seven questions (eligibility, size, float, who decides, timing, protection of current members, corporate actions) and sorting each relevant sentence into one of four kinds: hard rules you compute, discretion clauses you estimate, timing clauses that set the trade date, and exceptions that decide who is exempt.

The S&P 500 has ten entry screens, including $22.7bn of total market cap and positive earnings, but they apply only to new entrants, and the committee chooses among the candidates who pass them. Its timing clauses matter as much as its size rules: a 4% share offering looks like a quarterly event until the $1 billion exception makes it an accelerated one. The Russell indexes run a fixed sequence instead. They assign a home country, screen for a $1 price, $30 million size, 5% float, and 5% public votes, then rank by total market cap on rank day. A ±2.5-point band in cumulative market cap, worth $2.7bn to $9.6bn in June 2026, lets current members near the 1,000th-company cutoff stay put. That band is why predicting Russell moves needs the current membership list as well as the ranking, and why a "small-cap" company can be bigger than a "large-cap" one. Russell rebuilds in June (in full) and December (additions and migrations), and rank day is a measurement, not an announcement. Because the two rulebooks disagree on voting rights and profitability, the same company can qualify for one family and be barred from the other. The gap between what providers announce and what readers can compute is where desks compete.

## New Terms

**methodology document (rulebook)**: The index provider's official, versioned description of how an index is built and maintained.

**home country indicators (HCIs)**: The three facts Russell uses to assign a country: country of incorporation, country of headquarters, and country of the most-traded listing.

**benefit-driven incorporation (BDI) country**: A country where companies incorporate mainly for tax or legal reasons. Russell does not treat it as a real home country when assigning nationality.

**voting-rights test**: Russell's requirement that at least 5% of a company's total votes be held by the public.

**cumulative percentile (of market cap)**: For a company in a list sorted from largest to smallest, the running total of market cap up to and including that company, divided by the market total. Lower means bigger.

**breakpoint**: The company at an index boundary, such as #1,000 for the Russell 1000/2000 split.

**band (banding)**: A zone around a breakpoint in which current members keep their index assignment, to avoid needless turnover.

**preliminary list**: Russell's first published list of proposed additions, deletions, and migrations, released four to five weeks before a rebuild takes effect.

**lock-down period**: The final weeks before a Russell rebuild, during which membership is treated as final.

**reconstitution day**: The day a Russell rebuild takes effect, after the close. Index funds trade in that day's closing auction.

**quarterly rebalance**: For the S&P 500, the scheduled update after the close on the third Friday of March, June, September, and December.

**query period**: The two weeks after Russell's preliminary lists during which the market can report data errors.

**Russell 3000E**: The broadest Russell US index, the largest 4,000 eligible companies. All the other Russell US indexes are subsets of it.

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

1. A current Russell 2000 member ranks 990 on rank day, at a cumulative percentile inside the band. Where does it go, and why?

It stays in the Russell 2000. It is a current member inside the band, so the band overrides its rank. Its growth isn't treated as "material and sustained" yet.

2. Why does a desk need the current membership list, not just the rank-day ranking, to predict Russell migrations?

The band only protects current members. Two companies with the same rank can land in different indexes depending on where they are today.

3. A company has 50m public class A votes out of 900m total votes. Does it pass Russell's voting test?

Yes, barely: 50m / 900m = 5.6%, which is at least 5%. Passing this one test doesn't make it eligible, though. It still has to pass every other screen.

4. Why can a $36bn company be an S&P 500 candidate but excluded from every Russell index?

Russell requires at least 5% of votes in public hands, and S&P has no voting test. A super-voting share class can push public votes below 5% while the company still passes all of S&P's screens.

5. Why is the December Russell rebuild usually smaller than June's?

December only processes additions and moves between the size indexes. Float updates are limited to material changes with a buffer, and existing members' voting rights aren't reviewed.

6. An S&P 500 member sells new shares equal to 3% of its share count, raising $1.4bn. Is the change accelerated or quarterly?

Accelerated. It fails the 5% test, but S&P accelerates any event of at least $1 billion regardless of the 5% threshold.

7. A methodology sentence says "constituent selection is at the discretion of the Index Committee." What kind of sentence is it, and how should a desk treat the resulting flow?

It is a discretion clause. The flow can't be computed until the announcement, so the desk works with probabilities and prepares to react quickly when changes are announced.

8. What does a buffer gain, and what does it give up?

It cuts turnover and forced trading for index funds near a cutoff. In exchange, the index stops being an exact picture of the market, so a "small-cap" index can contain companies larger than some "large-cap" members.

9. Where would you look in S&P's documents to learn how a spin-off is treated, and what would you find?

In the Equity Indices Policies & Practices document, not the main U.S. Indices Methodology. It says the spin-off is added at a price of zero with no divisor change, then removed after at least one day if it isn't eligible, which creates forced selling.

## Sources

S&P Dow Jones Indices. "S&P U.S. Indices Methodology." July 2026. Eligibility Criteria, Index Construction, and Timing of Changes sections. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)

FTSE Russell. "Russell US Equity Indexes: Construction and Methodology." v7.2, August 2026. Sections 4–7 and Appendix F. [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf)

FTSE Russell. "FTSE Russell Announces 2026 Russell US Indexes Reconstitution Schedule." Press release, March 2, 2026. [https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule](https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule)

FTSE Russell. "2025 Russell Reconstitution Recap." [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf)

S&P Dow Jones Indices. "Equity Indices Policies & Practices Methodology." August 2026. Material Share/IWF Changes (Accelerated Implementation Rule) and Announcement Policy. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf)

S&P Dow Jones Indices. "Index Mathematics Methodology." September 2026. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf)

Gupta, Abhishek, Pavlo Taranenko, and Sebastien Lieblich. "Index Rebalancing During High Volatility: A Balancing Act." MSCI, May 13, 2020. [https://www.msci.com/research-and-insights/blog-post/index-rebalancing-during-high-volatility-a-balancing-act](https://www.msci.com/research-and-insights/blog-post/index-rebalancing-during-high-volatility-a-balancing-act)

CRSP. "Key Concepts" and "CRSP Market Indexes Methodology." [https://www.crsp.org/indexes/key-concepts/3/](https://www.crsp.org/indexes/key-concepts/3/) and [https://www.crsp.org/indexes/crsp-market-indexes-methodology/](https://www.crsp.org/indexes/crsp-market-indexes-methodology/)

Yoshimoto, Catherine. "Russell Reconstitution June 2026: Larger Leaders, Stronger Small Caps." FTSE Russell Insights, June 16, 2026. [https://www.lseg.com/en/insights/ftse-russell/russell-reconstitution-june-2026-larger-leaders-stronger-small-caps](https://www.lseg.com/en/insights/ftse-russell/russell-reconstitution-june-2026-larger-leaders-stronger-small-caps)

New Street IR. "Russell Reconstitution Now Happens Twice a Year." October 14, 2026. [https://newstreetir.com/2026/10/14/russell-reconstitution-now-happens-twice-a-year-what-does-that-mean-for-public-biotechs/](https://newstreetir.com/2026/10/14/russell-reconstitution-now-happens-twice-a-year-what-does-that-mean-for-public-biotechs/)

Li, Kun, Xin (Kelly) Liu, and Shang-Jin Wei. 2021. "Is Stock Index Membership for Sale?" NBER Working Paper 29365. [https://www.nber.org/papers/w29365](https://www.nber.org/papers/w29365)

Sharfman, Bernard S., and Vincent Deluard. 2021. "Discretionary Decision-Making and the S&P 500 Index." CLS Blue Sky Blog, March 30, 2021. [https://clsbluesky.law.columbia.edu/2021/03/30/discretionary-decision-making-and-the-sp-500-index/](https://clsbluesky.law.columbia.edu/2021/03/30/discretionary-decision-making-and-the-sp-500-index/)

Agrawal, Vidhi, Eesha Khalid, Tianyu Tan, and Doris Xu. 2024. "Hunting Tomorrow's Leaders: Using Machine Learning to Forecast S&P 500 Additions & Removal." arXiv:2412.12539. [https://arxiv.org/abs/2412.12539](https://arxiv.org/abs/2412.12539)

Greenwood, Robin, and Marco Sammon. 2025. "The Disappearing Index Effect." *Journal of Finance* 80 (2): 657-698. [https://www.nber.org/system/files/working_papers/w30748/w30748.pdf](https://www.nber.org/system/files/working_papers/w30748/w30748.pdf)
