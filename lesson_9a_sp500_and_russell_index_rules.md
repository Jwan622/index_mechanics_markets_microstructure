# Lesson 9a: Reading the S&P 500 and Russell Rulebooks

## Learning Goal

Lesson 8 claimed that index rules are public, and Lesson 9 summarized them. This module goes to the source. It walks through the actual rulebooks for the S&P 500 and the Russell US indexes, then applies them to four made-up companies, one rule at a time.

The skill being practiced is turning a sentence in a rulebook into a yes-or-no answer about a real company: is it eligible, which index does it go into, and when. On a flows desk, that answer comes before any estimate of how much will trade. A small clause, such as a voting-rights test or a band around a cutoff, can decide whether billions of dollars move or stay put.

## The Two Rulebooks

Each index family publishes a methodology document, which is the official rulebook. It is long, but only a few sections decide membership. These are the versions used in this lesson.

| Index | Document | Version |
|---|---|---|
| S&P 500 | S&P U.S. Indices Methodology | July 2026 |
| Russell | Russell US Equity Indexes: Construction and Methodology | v7.2, Aug 2026 |

The sections that matter:

| Question | S&P document | Russell document |
|---|---|---|
| Who is eligible? | Eligibility Criteria | Section 5 |
| How is size used? | Market Capitalization | Section 6 |
| How is float measured? | Float Adjustment Methodology | Section 7 |
| When do changes happen? | Timing of Changes | Appendix F |

Rulebooks change. Both documents above were revised in 2026: Russell moved to twice-yearly rebuilds, and S&P reviews its size threshold every quarter. Always check the version date before relying on a number.

Lesson 9 already covered the S&P 500's entry checklist. This module spends most of its time on the Russell rules, which Lesson 9 only sketched, and then runs both rulebooks against the same companies.

## Russell, Step 1: Is It a US Company?

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

## Russell, Step 2: The Eligibility Screens

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

## Russell, Step 3: Rank and Cut

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

## Russell, Step 4: The Band Around the Cutoff

### The problem the band solves

Suppose a company sits right at rank 1,000. One year it closes at rank 995 on rank day, the next at rank 1,005, then 998. With a hard cutoff, it would move between the Russell 1000 and the Russell 2000 every year. Lesson 9 showed that each move is a large net passive trade: in that example, $480 million of net selling on the way up. Nothing about the company changed in a meaningful way, yet index funds would keep churning the stock.

FTSE Russell's fix is a **band**. A *current* member near the cutoff keeps its index unless it has moved clearly past the line. The rulebook's goal is that companies show "material and sustained" growth or decline before they migrate.

### The measure: cumulative percentile

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

### The rule

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

### A worked example

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

### What the band does in real data

FTSE Russell's recap of the June 2025 reconstitution shows how much overlap the band creates. Both rows are after banding is applied:

| June 2025 | Company | Total cap |
|---|---|---:|
| Smallest Russell 1000 member | Newell Brands | $2.0bn |
| Largest Russell 2000 member | Ensign Group | $7.4bn |

The largest company in the "small-cap" index was more than three times the size of the smallest company in the "large-cap" index. A year later the range had grown with the market: FTSE Russell's June 2026 article put the breakpoint at $5.7bn and the band at $2.7bn to $9.6bn, with 97 Russell 2000 and 111 Russell 1000 members kept in place by it (preliminary data). Without banding, that couldn't happen, because every Russell 1000 company would be bigger than every Russell 2000 company. With banding, the boundary between the two indexes is a zone rather than a line, and current members on either side of the zone stay where they are. (This is why Lesson 9 said a Russell 2000 company is smaller than any Russell 1000 company "apart from the band.")

**Why is the real band so much wider than the worked example?** In the worked example, the band covered only a few dozen ranks on each side of 1,000: Birch at rank 960 was already outside it, and so was Dogwood at 1,060. In the real market it spans far more, because 2.5 points of *cumulative market cap* is a huge amount of value compared with the size of each company near the cutoff. A rough calculation with the 2025 recap's totals:

**Step 1. Total market value.** The recap gives $55.7tn for the Russell 1000 and $2.7tn for the Russell 2000, so about $58.4tn in all (ignoring the much smaller Microcap).

**Step 2. Value inside 2.5 points.**

> 2.5% × $58.4tn ≈ **$1.46tn**

**Step 3. Number of companies.** Companies near the cutoff are worth a few billion dollars each (between $2.0bn and $7.4bn in the table above). At around $4bn each:

> $1.46tn ÷ $4bn ≈ **365 companies** on each side of the breakpoint

So a current Russell 2000 member can grow well past rank 1,000 and still stay in the Russell 2000. This is a rough estimate, not a published figure, but it shows why the overlap in the table is so large.

## Russell, Step 5: The Timing

Russell rebuilds its indexes twice a year. Appendix F of the rulebook gives the rules, and the June 2026 dates come from FTSE Russell's published schedule.

| Stage | June rebuild | December rebuild |
|---|---|---|
| Rank day | last business day of April | last business day of October |
| Preliminary lists | 5 weeks before | 4 weeks before |
| Query period | 2 weeks after the lists | 2 weeks after the lists |
| Lock-down | 3 weeks before | 2 weeks before |
| Effective | after the close, 4th Friday of June | after the close, 2nd Friday of December |

What each stage means:

- **Rank day**: the measurement. Prices and shares are recorded at the close. Nothing is published.
- **Preliminary lists**: the first announcement of adds, deletes, and migrations.
- **Query period**: when the market can point out data errors.
- **Lock-down**: membership is treated as final.
- **Effective**: index funds trade in that day's closing auction, and the new index applies from the next open.

Applied to 2026. The June column is FTSE Russell's published schedule; the December column is worked out from the rules:

| Stage | June 2026 | December 2026 |
|---|---|---|
| Rank day | Thu 30 Apr | Fri 30 Oct |
| Preliminary lists | Fri 22 May | about Fri 13 Nov |
| Effective | Fri 26 Jun | Fri 11 Dec |

The December dates follow from Appendix F: 30 October is the last business day of October 2026, and 11 December is the second Friday of December. Market commentary (New Street IR, October 2026) reports the same dates, with preliminary lists on 13 November. Check FTSE Russell's official notice before trading on them.

**December is a smaller rebuild.** The December rebuild only handles new additions and moves between the Russell 1000, Russell 2000, and Microcap. Float changes are applied only if they are material, with a 3% buffer, and voting rights of existing members aren't re-checked. The full review of everything happens in June. So expect less turnover in December than in June.

## The S&P Side, Briefly

Lesson 9's entry checklist covered the S&P 500's eligibility rules. Two features of the S&P rulebook matter most when you compare it with Russell's.

First, there is **no rank day and no scheduled rebuild**. Changes are made as needed, announced with at least three business days' notice. The committee chooses among eligible candidates.

Second, **the screens apply to getting in, not to staying in**. A current member that fails a screen is not removed automatically. This is the S&P version of a band, and it is much wider than Russell's: a member can shrink far below the $22.7bn entry threshold and remain in the index. The rulebook also excuses MidCap 400 members being promoted to the S&P 500 from the profitability, liquidity, and float-size tests. They only need to meet the size rule.

So both families protect current members, but in different ways:

| | S&P 500 | Russell |
|---|---|---|
| Protection for members | Entry rules don't apply to current members | ±2.5-point band at the cutoff |
| How much protection | Large: removal is a committee choice | Limited: outside the band, you move |
| Effect on flow | Deletions are rare and hard to predict | Migrations are computable from rank and membership |

## Four Companies, Two Rulebooks

Each case lists the given facts, then checks the rules one at a time. All four companies are made up.

### Case A: Northwind Software (profitable enough?)

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

### Case B: Granite Holdings (super-voting shares)

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

### Case C: Cedar Industries (protected by the band)

Given: Cedar from the banding example, a current Russell 1000 member that ranks 1,020 at a cumulative percentile of 91.2%, with the band at 87.5–92.5%.

| Check | Answer |
|---|---|
| Is Cedar a current Russell 3000 member? | Yes, so the band applies |
| Is 91.2% inside 87.5–92.5%? | Yes |
| Result | Stays in the Russell 1000 |

Now change one fact. Suppose Cedar were a newly eligible company with the same rank and size. The band would not apply, and rank 1,020 would put it in the **Russell 2000**. Same company, same size, different index, depending only on whether it was already a member.

### Case D: Pebble Bio (the $1 rule)

Given: a current Russell 2000 member that closes at $0.92 on rank day. Its average closing price over the previous 30 days was $1.04.

| Check | Member rule | Pebble | Pass? |
|---|---|---|---|
| Rank-day close | ≥ $1.00, or else... | $0.92 | no |
| 30-day average | ≥ $1.00 | $1.04 | yes |

Because it is a current member, the 30-day average rescues it, and **Pebble stays eligible**. A newcomer closing at $0.92 would simply be ineligible, since the 30-day fallback only applies to current members.

## The Comparison Table

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

## Common Misconceptions

**"A company in the top 1,000 by size is in the Russell 1000."** Only if it is new to the Russell 3000 or outside the band. Alder ranked 985 and stayed in the Russell 2000. Membership depends on rank *and* on the current membership list.

**"Bigger companies always qualify for more indexes."** Granite is a $36bn company that is excluded from every Russell index because of its voting structure, while Northwind is excluded from the S&P 500 because of one bad year of earnings. Size is necessary but not sufficient.

**"A lower cumulative percentile means a smaller company."** It means the opposite. The running total starts from the largest company, so the biggest companies have the lowest percentiles.

**"The December rebuild is a repeat of June."** December only handles additions and size migrations, with lighter float updates and no voting-rights review of existing members. Expect less turnover.

**"The S&P 500 removes companies that fail the rules."** The rules are for entry. Removal is a committee decision, usually triggered by an acquisition or by a company becoming clearly unrepresentative.

## Recap

The rulebooks are where index flows start. The Russell indexes run a fixed sequence. First they assign a home country using three indicators. Then they screen for a $1 price, $30 million size, 5% float, and 5% public voting rights. They rank by total market cap on rank day, and they protect current members near the 1,000th-company cutoff with a ±2.5-point band measured in cumulative percentile of market cap. Because of that band, you need both the ranking and the current membership list to predict who migrates. A newcomer and a current member of the same size can end up in different indexes. Russell rebuilds in June (full review) and December (additions and migrations only), on dates fixed by rule. The S&P 500 has no rebuild, and its committee picks from eligible candidates. Its screens apply only to new entrants, which protects existing members far more than Russell's band does. The two rulebooks disagree on voting rights and profitability, so the same company can qualify for one family and be barred from the other.

## New Terms

**methodology document (rulebook)**: The index provider's official, versioned description of how an index is built and maintained.

**home country indicators (HCIs)**: The three facts Russell uses to assign a country: country of incorporation, country of headquarters, and country of the most-traded listing.

**benefit-driven incorporation (BDI) country**: A country where companies incorporate mainly for tax or legal reasons. Russell does not treat it as a real home country when assigning nationality.

**voting-rights test**: Russell's requirement that at least 5% of a company's total votes be held by the public.

**cumulative percentile (of market cap)**: For a company in a list sorted from largest to smallest, the running total of market cap up to and including that company, divided by the market total. Lower means bigger.

**breakpoint**: The company at an index boundary, such as #1,000 for the Russell 1000/2000 split.

**band (banding)**: A zone around a breakpoint in which current members keep their index assignment, to avoid needless turnover.

**query period**: The two weeks after Russell's preliminary lists during which the market can report data errors.

**Russell 3000E**: The broadest Russell US index, the largest 4,000 eligible companies. All the other Russell US indexes are subsets of it.

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

## Sources

S&P Dow Jones Indices. "S&P U.S. Indices Methodology." July 2026. Eligibility Criteria, Index Construction, and Timing of Changes sections. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)

FTSE Russell. "Russell US Equity Indexes: Construction and Methodology." v7.2, August 2026. Sections 4–7 and Appendix F. [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf)

FTSE Russell. "FTSE Russell Announces 2026 Russell US Indexes Reconstitution Schedule." Press release, March 2, 2026. [https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule](https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule)

FTSE Russell. "2025 Russell Reconstitution Recap." [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/other/2025-russell-recon-recap-final.pdf)
