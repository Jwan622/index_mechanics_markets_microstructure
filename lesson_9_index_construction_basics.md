# Lesson 9: Index Construction Basics

## Learning Goal

Lesson 8 said an index fund must hold what its index holds, at the index's weights. This lesson explains where those weights come from: how an index provider takes a few public facts about each company and turns them into a list of stocks and percentages.

The reason this matters on a desk is that those facts change. A company issues new shares, buys some back, or a founder sells a big stake. When an input changes, the weights change. Then every fund copying the index has to trade, even though nobody has a view on the stock.

## What an Index Is

An index is a number that summarizes how a group of stocks did. It is defined by two things:

1. **A list of members**: which stocks count.
2. **A weight for each member**: how much each stock's move counts toward the total.

The index's return is the weighted average of its members' returns. Here is a two-stock index:

| Stock | Weight | Return today | Contribution (weight × return) |
|---|---:|---:|---:|
| A | 75% | +2% | 0.75 × 2% = +1.5% |
| B | 25% | −4% | 0.25 × −4% = −1.0% |
| **Index** | 100% | | **+0.5%** |

B fell twice as much as A rose, but the index still went up, because A counts three times as much. The weights decide what "the market" did.

Now a fund with $100 that wants to track this index buys $75 of A and $25 of B. Its return today is $75 × 2% − $25 × 4% = $1.50 − $1.00 = $0.50, which is +0.5%, matching the index exactly. That is all index tracking is: **hold each stock in proportion to its weight.**

So everything comes down to where the weights come from. Index providers answer two questions:

- **Eligibility**: which stocks are allowed in? (Big enough? Liquid enough? US-based?)
- **Weighting**: how big is each member's share? For most major indexes, the answer is "in proportion to the value of the company's shares that investors can actually buy."

```text
company facts (price, shares, who owns them, earnings, volume)
   |
   v
eligibility rules  ->  which stocks are in
   |
   v
weighting rule     ->  each member's weight
   |
   v
target weights     ->  what every tracking fund must hold
```

## Why Share Counts and Ownership Change the Weights

The rest of the lesson builds this step by step, but here is the punchline first.

Under the usual rule, a stock's weight is its **buyable value** divided by the total buyable value of all members. Buyable value is price × the number of shares that investors can actually trade. Anything that changes that number changes the weight, even when the stock price doesn't move:

| Event | What happens to buyable shares | Weight | What tracking funds do |
|---|---|---|---|
| Company issues new shares | more shares exist | up | buy |
| Company buys back shares | fewer shares exist | down | sell |
| Founder sells a large block to the public | shares move from "locked up" to "tradable" | up | buy |
| Stock joins the index | goes from no weight to some weight | up from 0 | buy |

The founder case is the least obvious. The company's total value doesn't change when a founder sells. The same shares exist, at the same price. What changes is *who holds them*. While the founder held the shares, they were not for sale, so the index excluded them. Once they're sold to the public, they are tradable, so the index counts them. That gives the stock a bigger weight, and index funds must buy their slice of the newly tradable shares. The sections below define these terms properly and work through the numbers.

## Market Capitalization: The Starting Point

A company's **market capitalization**, or market cap, is the market value of all its shares:

```text
market cap = share price × shares outstanding
```

A company with 200 million shares at $50 has a market cap of $10 billion. Most major equity indexes, including the S&P 500 and the Russell indexes, start from market cap because it measures how much of the stock market a company represents. If you owned every share of every company, each company's share of your wealth would be its market cap divided by the total.

## Free Float: Not Every Share Can Be Bought

Market cap counts every share, but some shares are not really available. A founder might hold 60% of a company and have no plans to sell. A government might own a stake in a national champion. Another company might hold a controlling block. Those shares exist, but an index fund cannot buy them.

The shares that ordinary investors can actually buy and sell are called the **free float**. Index providers adjust for this with a **float factor**, the fraction of shares counted as available. S&P Dow Jones Indices calls theirs the **investable weight factor (IWF)**. Its float methodology treats blocks held by insiders, founders and their family trusts, other public companies, and government agencies as strategic. It counts those blocks as unavailable when they reach 5% or more of the shares.

```text
float-adjusted market cap = price × shares outstanding × float factor
```

This is the formal name for the "buyable value" used above. The company above, with a founder holding 60%, has a float factor of 0.40. Its float-adjusted market cap is $10 billion × 0.40 = $4 billion.

Why bother? Without the adjustment, an index would give the company a weight based on $10 billion, and index funds would try to buy shares worth $10 billion of exposure from a pool of only $4 billion. They would end up competing for the same scarce shares. Float adjustment makes the index ask only for what can actually be bought. Both the S&P 500 and the Russell US indexes weight their members by float-adjusted market cap.

## A Three-Stock Toy Index

Here is a small index built step by step. The numbers are made up, but the arithmetic is exactly the method real cap-weighted indexes use.

| Stock | Price | Shares outstanding | Float factor | Why |
|---|---:|---:|---:|---|
| A | $50 | 200m | 1.00 | widely held |
| B | $100 | 100m | 0.40 | founder owns 60% |
| C | $20 | 300m | 0.90 | a parent company owns 10% |

**Step 1. Market cap = price × shares outstanding.**

| Stock | Calculation | Market cap |
|---|---|---:|
| A | $50 × 200m | $10.0bn |
| B | $100 × 100m | $10.0bn |
| C | $20 × 300m | $6.0bn |
| **Total** | | **$26.0bn** |

**Step 2. Float-adjusted market cap = market cap × float factor.**

| Stock | Calculation | Float-adjusted cap |
|---|---|---:|
| A | $10.0bn × 1.00 | $10.0bn |
| B | $10.0bn × 0.40 | $4.0bn |
| C | $6.0bn × 0.90 | $5.4bn |
| **Total** | | **$19.4bn** |

**Step 3. Weight = each stock's float-adjusted cap ÷ the total.**

The weight answers one question: *out of all the tradable value in the index, what fraction belongs to this stock?* The total tradable value is $19.4bn, and A accounts for $10.0bn of it.

| Stock | Its tradable value | ÷ Total | Weight |
|---|---:|---:|---:|
| A | $10.0bn | $19.4bn | 51.5% |
| B | $4.0bn | $19.4bn | 20.6% |
| C | $5.4bn | $19.4bn | 27.8% |

The weights add up to 100%. Read them as "out of every $100 in a tracking fund, $51.50 goes into A, $20.60 into B, and $27.80 into C."

Now look at B. A and B are both $10bn companies. But 60% of B is locked up with its founder, so only $4bn of B is tradable. The index counts only the tradable part, so B's weight (20.6%) is well under half of A's (51.5%).

### What a fund tracking this index holds

Give a fund $1 billion to track the index and work out its holdings one step at a time.

**Step 4. Dollars in each stock = weight × $1 billion.**

| Stock | Weight | × Fund size | Dollars held |
|---|---:|---:|---:|
| A | 51.5% | $1,000m | $515m |
| B | 20.6% | $1,000m | $206m |
| C | 27.8% | $1,000m | $278m |

So about half of the fund's $1 billion ($515m) goes into A, because A is about half of the index. About 20% ($206m) goes into B and about 28% ($278m) into C. These percentages are the **weights**, and they describe how the fund splits its own money.

**Step 5. Shares held = dollars ÷ price.**

| Stock | Dollars held | ÷ Price | Shares held |
|---|---:|---:|---:|
| A | $515m | $50 | 10.3m |
| B | $206m | $100 | 2.06m |
| C | $278m | $20 | 13.9m |

**Step 6. What fraction of each company's tradable shares does the fund own?** This step looks at the company's side, not the fund's. Take the shares the fund holds and divide by all the tradable shares that exist (shares outstanding × float factor).

| Stock | Fund holds | Tradable shares | Fund's share |
|---|---:|---:|---:|
| A | 10.3m | 200m × 1.00 = 200m | 5.2% |
| B | 2.06m | 100m × 0.40 = 40m | 5.2% |
| C | 13.9m | 300m × 0.90 = 270m | 5.2% |

(A: 10.3 / 200. B: 2.06 / 40. C: 13.9 / 270.)

The fund ends up owning **5.2% of the tradable shares of every company**. A, B, and C have different prices, sizes, and founders, but the fund owns the same slice of each.

This 5.2% is *not* how much of the fund's $1 billion goes into each stock. That was Step 4: 51.5% into A, 20.6% into B, 27.8% into C. Two different questions are being answered:

| Question | Answer | Same for all? |
|---|---|---|
| How much of the *fund's money* is in this stock? | the weight (51.5%, 20.6%, 27.8%) | No |
| How much of *this company's tradable shares* does the fund own? | 5.2% | Yes |

### Why the slice is the same for every stock

It looks like a coincidence that A, B, and C all come out at 5.2%, but it isn't. Follow stock A through two steps.

**Step 1. How many dollars does the fund put into A?** A's weight times the fund size:

> dollars in A = **$10.0bn** / $19.4bn × $1bn = $515m

**Step 2. What fraction of A's tradable value is that?** Divide those dollars by A's tradable value, $10.0bn:

> fraction of A owned = ( **$10.0bn** / $19.4bn × $1bn ) / **$10.0bn**

**Step 3. Cancel.** A's $10.0bn appears once on top (from its weight) and once on the bottom (its size), so the two cancel:

> fraction of A owned = $1bn / $19.4bn = **5.2%**

A's own size has dropped out. All that's left is the fund size divided by the index total, and those two numbers are the same for every stock. Run B through the same steps and its $4.0bn cancels the same way:

| Stock | Dollars in the stock | ÷ Its tradable value | = Fraction owned |
|---|---:|---:|---:|
| A | $10.0bn / $19.4bn × $1bn = $515m | $10.0bn | 5.2% |
| B | $4.0bn / $19.4bn × $1bn = $206m | $4.0bn | 5.2% |
| C | $5.4bn / $19.4bn × $1bn = $278m | $5.4bn | 5.2% |

In words: a big stock gets more of the fund's dollars, but it also has more tradable shares to spread them across. Weighting by tradable value makes those two effects match exactly, so every stock ends up with the same slice: **fund size ÷ total tradable value of the index**.

### Why this is useful on a desk

This ratio gives a quick estimate of index flow. Add up all the money tracking an index and divide by the index's total tradable value. Call the answer X. Then:

- index trackers own about X% of the tradable shares of every member, and
- when a stock is added, trackers must buy about X% of its tradable shares.

For example, suppose stock D joins the toy index. D has a $40 price, 100m shares, and a float factor of 0.50, so it has 50m tradable shares worth $2.0bn. The index's total tradable value becomes $19.4bn + $2.0bn = $21.4bn, so X = $1bn / $21.4bn = 4.7%.

| | Calculation | Result |
|---|---|---:|
| Tradable shares of D to buy | 4.7% × 50m | about 2.3m shares |
| Dollar cost | 2.3m × $40 | about $93m |

The fund pays for D by selling a little of A, B, and C, whose slices drop from 5.2% to 4.7%.

Keep two numbers separate here. The **weights** say how the fund's dollars are split. They differ by stock and always add up to 100%. **X** says how much of each company's tradable shares the fund owns, and it is the same for every stock. When D joins, both change together:

| Stock | Weight before | Weight after | Fund's slice |
|---|---:|---:|---:|
| A | 51.5% | 46.7% | 5.2% → 4.7% |
| B | 20.6% | 18.7% | 5.2% → 4.7% |
| C | 27.8% | 25.2% | 5.2% → 4.7% |
| D | — | 9.3% | 0% → 4.7% |
| **Total** | 100% | 100% | |

Lesson 14 refines this estimate with real indexed-asset numbers, but the logic is exactly this.

## Why Cap Weighting Rarely Forces Trades and Equal Weighting Often Does

Suppose stock A rises 10% tomorrow and nothing else moves. In a cap-weighted index, A's weight rises because its market cap rose. The fund's A shares also rose 10%, so its holdings already match the new weights. **The fund does not need to trade.** Price moves rebalance a cap-weighted portfolio automatically.

An **equal-weighted index** gives every member the same weight, here 33.3% each, regardless of size. After A rises 10%, the fund's A position is now more than one third of the portfolio. To get back to equal weights, the fund must sell some A and buy B and C. Equal-weighted indexes therefore rebalance on a fixed schedule; the S&P 500 Equal Weight Index, for example, resets to equal weights each quarter. Every rebalance date is a predictable trade, which sells recent winners and buys recent losers.

| Weighting scheme | When prices move | Result |
|---|---|---|
| Cap weighting | holdings and target weights move together | no trade needed |
| Equal weighting | holdings drift away from equal | trade at each scheduled rebalance |

The three schemes give very different portfolios from the same three stocks. Each one divides by a different total:

| Scheme | What each stock is measured by | Total | A | B | C |
|---|---|---:|---:|---:|---:|
| Float-adjusted cap | tradable value (Step 2) | $19.4bn | 10.0 / 19.4 | 4.0 / 19.4 | 5.4 / 19.4 |
| Total cap | all shares, no float adjustment (Step 1) | $26.0bn | 10.0 / 26.0 | 10.0 / 26.0 | 6.0 / 26.0 |
| Equal | nothing, every stock counts the same | 3 stocks | 1 / 3 | 1 / 3 | 1 / 3 |

Under total cap, A and B both get 38.5%, because both are $10bn companies when every share is counted. The founder's locked-up 60% of B counts here. Float adjustment removes it, which is why B drops to 20.6% in the first column.

| Stock | Float-adjusted cap weight | Total cap weight | Equal weight |
|---|---:|---:|---:|
| A | 51.5% | 38.5% | 33.3% |
| B | 20.6% | 38.5% | 33.3% |
| C | 27.8% | 23.1% | 33.3% |

A common mistake is to think cap-weighted index funds never trade. They trade whenever something other than price changes the recipe: membership changes, share issuance or buybacks, float changes, and the corporate actions covered in Lesson 10.

## When the Recipe Changes, Funds Trade

Return to the $1 billion fund. B's founder held 60% of B and now sells half of that stake (30% of the company) to the public. Before, 40% of B's shares were tradable. Now 40% + 30% = 70% are, so B's float factor rises from 0.40 to 0.70. Prices don't change, and the fund is still $1 billion.

Follow B through the steps.

**Step 1. What is B's new tradable value?** Multiply market cap by the new float factor.

| | Market cap | × Float factor | = Tradable value |
|---|---:|---:|---:|
| B before | $10.0bn | 0.40 | $4.0bn |
| B after | $10.0bn | 0.70 | $7.0bn |

**Step 2. What is the index's new total tradable value?** Only B changed, so A and C stay the same.

| | A | + B | + C | = Total |
|---|---:|---:|---:|---:|
| Before | $10.0bn | $4.0bn | $5.4bn | $19.4bn |
| After | $10.0bn | $7.0bn | $5.4bn | $22.4bn |

**Step 3. What is B's new weight?** Divide B's tradable value by the total.

> B's new weight = $7.0bn / $22.4bn = **31.25%** (it was $4.0bn / $19.4bn = 20.6%)

**Step 4. How many dollars should the fund now hold in B?** Multiply the weight by the fund size.

> B's new holding = 31.25% × $1,000m = **$312.5m**, which rounds to $313m

**Step 5. What does the fund have to trade?** Subtract what it already holds.

> trade in B = $312.5m − $206m = **buy about $106m**

At $100 a share, that is about 1.06m more shares of B.

**Step 6. Where does the money come from?** The fund has no new cash, so it sells A and C. Their tradable values didn't change, but the total grew, so their weights fell. Doing Steps 3–5 for every stock:

| Stock | New weight | New holding | Old holding | Trade |
|---|---:|---:|---:|---|
| A | 10.0 / 22.4 = 44.6% | $446m | $515m | sell $69m |
| B | 7.0 / 22.4 = 31.3% | $313m | $206m | **buy $106m** |
| C | 5.4 / 22.4 = 24.1% | $241m | $278m | sell $37m |

The sales ($69m + $37m = $106m) pay for the purchase exactly.

**A second way to see it.** Use the fund's slice from earlier. The slice was $1bn / $19.4bn = 5.2% of every company's tradable shares. Now it is $1bn / $22.4bn = 4.46%. B has 100m × 0.70 = 70m tradable shares, so the fund should own 4.46% × 70m = 3.125m shares, worth 3.125m × $100 = $312.5m. That's the same answer. The fund's slice of *every* company shrank a little, but B's tradable share count grew a lot (40m → 70m), so the fund ends up holding more B.

Nothing about B's business changed, and the fund has no opinion. A change in *who owns the shares* moved $106 million into B. Scale that up from $1 billion to the hundreds of billions that track a major index, and an ownership change becomes a flow event. Lesson 12 covers these weight changes in detail.

## Eligibility: Who Gets In

Weighting only applies to members, so the membership rules matter just as much. Most index families combine several kinds of screens.

A **size screen** sets how large a company must be. It can be a fixed threshold ("market cap at least $X") or a rank ("the largest 1,000 companies"). A **liquidity screen** requires enough trading that funds can buy and sell without huge cost, measured for example by shares traded per month or by annual dollar volume relative to market cap. A **float screen** excludes companies with too few shares available. **Domicile and security-type rules** decide what counts as a "US company" and exclude things like ETFs and closed-end funds. Some indexes add a **financial-viability** screen. The S&P 500, for example, requires positive reported earnings over the most recent quarter and over the trailing four quarters combined.

The two big US families make an instructive contrast:

| | S&P 500 | Russell 1000 / 2000 / 3000 |
|---|---|---|
| **Who decides** | An index committee, applying published criteria with some discretion | Mechanical ranking by total market cap on rank day |
| **How size is used** | Minimum thresholds | Rank cutoffs: largest 1,000, next 2,000, combined 3,000 |
| **When changes happen** | As needed during the year, plus quarterly rebalances | At reconstitution: annually each June since 1989, moving to twice a year from December 2026 |
| **Weighting** | Float-adjusted market cap | Float-adjusted market cap |

Note the Russell detail: stocks are *ranked* by total market cap but *weighted* by float-adjusted cap. A company with a large founder stake can rank inside the Russell 1000 by total size and still get a small weight.

### What "mechanical ranking by total market cap on rank day" means

Each word does work. *Total market cap* means price × all shares outstanding, before any float adjustment. *Rank day* is a single date on which FTSE Russell takes a snapshot of every eligible company's total market cap at that day's close. *Mechanical ranking* means it sorts those companies from largest to smallest and applies fixed cutoffs. Positions 1 to 1,000 go to the Russell 1000, and positions 1,001 to 3,000 go to the Russell 2000. Nobody votes. The rule is a sorting step that anyone with the same data could run.

### What the Russell names mean

The names are misleading, so it's worth being exact. **The number in the name is how many companies the index holds, not the last rank it reaches.** The Russell 2000 is *not* ranks 1–2,000. It is 2,000 companies: ranks 1,001 to 3,000.

Everything starts from one ranked list. On rank day, FTSE Russell sorts every eligible US company by total market cap. The largest 4,000 form the broadest index, the **Russell 3000E**, and every other Russell US index is a slice of that list. The rulebook (Section 6.10) defines the slices:

| Index | Ranks | Companies | Segment |
|---|---|---:|---|
| Russell 3000E | 1 – 4,000 | 4,000 | the whole list |
| Russell 3000 | 1 – 3,000 | 3,000 | broad market |
| Russell 1000 | 1 – 1,000 | 1,000 | large and mid cap |
| Russell 2000 | 1,001 – 3,000 | 2,000 | small cap |
| Russell Microcap | 2,001 – 4,000 | 2,000 | micro cap |
| Russell Top 200 | 1 – 200 | 200 | mega cap |
| Russell Midcap | 201 – 1,000 | 800 | mid cap |
| Russell 2500 | 501 – 3,000 | 2,500 | small and mid cap |

The first five are the ones a flows desk meets most. As a picture, with rank increasing to the right (bigger companies on the left):

```text
rank:  1            1,000          2,000          3,000          4,000
       |--------------|--------------|--------------|--------------|
       [ Russell 1000 ][        Russell 2000        ]
       [                Russell 3000                ]
                                     [       Russell Microcap      ]
       [                       Russell 3000E                       ]
```

Four things to read off it:

1. **The Russell 1000 and Russell 2000 never share a company.** Together they make up the Russell 3000: 1,000 + 2,000 = 3,000.
2. **The Russell 2000 and the Microcap *do* overlap.** Ranks 2,001–3,000 are the bottom half of the Russell 2000 *and* the top half of the Microcap. Here the name "Microcap" refers to size, and its count is again 2,000 (ranks 2,001–4,000).
3. **The Russell 3000E is the Russell 3000 plus ranks 3,001–4,000.** Those extra 1,000 companies are the smallest ones, in the Microcap only.
4. **Every index has its own funds.** A company at rank 1,500 sits in the Russell 2000, the Russell 3000, the Russell 2500, and the Russell 3000E at once. Any fund tracking any of those holds it.

One caveat on the boundaries: the ranks in the table are where the lines fall for *new* companies. At the 1,000 boundary (and at 200, 500, and 2,000), current members get some room through the band described in "The rebuild and the band" below. At 3,000 and 4,000 the rulebook applies no band, so those lines are hard.

So the Russell 2000 is the small-cap index. With a pure rank cutoff, every Russell 2000 company would be smaller than every Russell 1000 company. In practice the two overlap, because of a rule called the **band**, explained in "The rebuild and the band" below.

A tiny version: suppose there were only five eligible companies and the "large-cap" index took the top two.

| Company | Price | Shares | Total cap | Rank | Index |
|---|---:|---:|---:|---:|---|
| P | $80 | 500m | $40bn | 1 | large-cap |
| Q | $25 | 1,200m | $30bn | 2 | large-cap |
| R | $60 | 400m | $24bn | 3 | small-cap |
| S | $10 | 2,000m | $20bn | 4 | small-cap |
| T | $45 | 300m | $13.5bn | 5 | small-cap |

If R had closed at $80 on rank day instead of $60, its cap would be $32bn. It would rank second, move into the large-cap index, and push Q down. The rank-day closing price decides membership. (This is the rule for a company that is *new* to the index. Current members near the cutoff are treated differently, as "The rebuild and the band" below explains.)

### The important dates

**Russell (2026 June reconstitution, from FTSE Russell's published schedule):**

| Date | Event | What it means |
|---|---|---|
| Thu 30 Apr | **Rank day** | Total market caps are measured at the close. This is the measurement date, *not* an announcement. Nothing is published yet. |
| Fri 22 May | **Preliminary lists** | FTSE Russell publishes the proposed additions and deletions after 6 p.m. ET. This is the first official announcement. |
| Fri 29 May, 5 Jun, 12 Jun, Thu 18 Jun | **Updates** | Revised lists that fix data errors and reflect corporate actions such as IPOs and mergers. |
| Mon 8 Jun | **Lock-down begins** | Membership is considered final. After this, the list is not expected to change. |
| Fri 26 Jun | **Reconstitution day** (effective) | Index funds trade in the closing auction, and the new index applies from this close. |
| Mon 29 Jun | **First day of the new index** | Markets open with the reconstituted indexes. |

So, to answer the obvious question directly: Russell does *not* announce additions on the last day of April. That day is when the *measurement* happens. The first official list comes about three weeks later, and the trade happens about two months later. Until 2026 this happened once a year, in June. From 2026 there is a second rebuild each December: rank day is the last business day of October (30 October 2026), preliminary lists follow on 13 November, and the changes take effect after the close on 11 December 2026.

**S&P 500:**

| Timing | Event | What it means |
|---|---|---|
| Monthly meetings, but no scheduled reconstitution | **Committee decision** | The committee picks additions from eligible candidates, often to replace a company leaving after an acquisition. S&P's methodology says changes are made "on an as-needed basis." |
| At least 3 business days before the effective date | **Announcement** | S&P publishes the change on its website. The methodology requires at least three business days' notice, and the committee may give less. This is the first time the market knows for sure. |
| After the close on the third Friday of March, June, September, and December | **Quarterly rebalance** | Share counts are updated, and many membership changes are timed to take effect then. Index funds trade in that day's closing auction. |
| Any date | **Off-cycle change** | A merger, acquisition, or bankruptcy can trigger a replacement outside the quarterly schedule. |

### The rebuild and the band

Two words in the Russell rules need to be pinned down: *rebuild* and *band*.

**The rebuild.** FTSE Russell calls it **reconstitution**: every company is re-ranked from scratch, and every index's membership is set again. It now happens twice a year:

| Rebuild | Rank day | Effective | Reviews |
|---|---|---|---|
| June | last business day of April | 4th Friday of June | everything |
| December | last business day of October | 2nd Friday of December | new adds and moves between indexes |

Rank day is when caps are measured, and the effective date is when index funds trade at the close. The June rebuild is the full review. The December rebuild is lighter: under the rulebook (Appendix F), it handles new additions and moves between the Russell 1000, Russell 2000, and Microcap, but it only updates float for material changes and doesn't re-check existing members' voting rights. Between rebuilds, the only membership changes are quarterly IPO additions and corporate events such as mergers.

**The band.** Yes, there is one. It is in Section 6.10 of the current rulebook (version 7.2, August 2026), which says a band is placed around the market-cap breakpoint "to avoid unnecessary turnover at reconstitution." The section applies to reconstitution in general, so it covers both rebuilds.

The problem it solves: a company sitting right at rank 1,000 would otherwise flip between the Russell 1000 and Russell 2000 at every rebuild, as its rank wobbled between 995 and 1,005. Each flip forces a large index trade (see "Moving *up* from the Russell 2000 can mean being *sold*" below), even though the company barely changed.

The rule treats new and current members differently:

- A **new** company goes by the breakpoint alone: above it means Russell 1000, below it means Russell 2000.
- A **current** member stays in its index as long as it is inside the band around the breakpoint. It only moves if it ends up clearly past the line.

Technically the band is measured in *cumulative percentile of market cap* (±2.5 points). Lesson 9a works through that measure step by step. In practice, FTSE Russell translates it into a range of market caps. Its June 2026 article gives the real numbers:

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

### Why one is forecastable and the other isn't

Russell's rule is mechanical, so it *can* be computed in advance. As soon as rank day closes, a trader with price and share-count data can sort the companies and get very close to the preliminary list, three weeks before FTSE Russell publishes it. Even before rank day, they can estimate it, with uncertainty only about how prices will move before April 30. That is why Russell flow is crowded early. Many desks are running the same sort.

The S&P 500 is different. Being eligible (large enough, profitable, liquid, enough float) only makes a company a *candidate*. The committee then chooses among candidates, considering things like sector balance, and often acts only when a seat opens up. Traders can rank candidates by how likely they are to be picked, but they cannot know who is added until S&P announces. So for S&P, the main price move tends to come on the announcement. For Russell, much of it can come before the official list.

### Can the S&P committee be predicted?

Partly. The committee is a group of people, not a hidden algorithm. S&P's methodology says its members are full-time S&P Dow Jones Indices staff who meet monthly. They review candidates for addition, sector composition, and pending corporate actions, and "all Index Committee discussions are confidential." The published criteria screen the candidates, and the members then use judgment. Researchers have looked at how much that judgment matters. Li, Liu, and Wei (2021) find "a nontrivial amount of discretion" in S&P 500 membership. Their most striking result is that firms buying S&P credit ratings seem to have a better chance of being added, while buying Moody's ratings shows no such effect. Sharfman and Deluard (2021) point to discretionary choices with big consequences, such as excluding new dual-class companies from 2017. The current methodology no longer has that exclusion: it includes each listed share class separately. They also argue that Tesla would have qualified years before its 2020 addition under a size-only rule, although the profitability test is part of why it waited.

Discretion does not mean randomness, though. A committee that makes many similar decisions leaves a pattern, and that pattern can be learned. This is a natural machine-learning problem: a classifier estimates the probability that each candidate is added next quarter. Agrawal and coauthors (2024) train a random forest on quarterly financial, market, industry, and governance data and report a test F1 score of 0.85. F1 combines how many predicted adds were right with how many real adds were caught. Useful features follow directly from how the committee works:

| Feature | Why it should matter |
|---|---|
| Size relative to the smallest current members | A candidate has to look like it belongs |
| Positive earnings, liquidity, float | Published eligibility screens |
| Sector weight in the index vs the market | The committee considers sector balance |
| Being a large member of the S&P MidCap 400 | Many additions are promotions from the MidCap |
| Seats opening (members being acquired) | Additions often happen only when someone leaves |

Three things limit how far a model can go. First, the model can rank candidates, but *timing* depends on when a seat opens, which usually comes from an unrelated merger. Second, there are only a few additions each quarter, so even a good model has to pick from a handful of close candidates, and the evaluation must use a time-based split with data as it was known at the time (Lessons 24–26). Third, everyone can build the same model. Greenwood and Sammon (2025) show that the average S&P 500 addition effect fell from about 7.4% in the 1990s to under 1% in the last decade. Two reasons they give are that changes are more anticipated and that more additions are MidCap promotions, where the buying and selling partly offset. A good forecast is now partly priced in, so the edge comes from being better calibrated or faster than the crowd, not from forecasting at all. Lesson 15 builds a rules-based version of this, and Lesson 25 adds the machine learning.

### Other differences that matter for flow

The table above covers the rules. Four more differences change how the flow behaves.

**Moving *up* from the Russell 2000 can mean being *sold*.** This is the most counterintuitive one. It uses the rule from the toy index: trackers own the same slice of every member's tradable shares, and that slice = money tracking the index ÷ the index's total tradable value.

The numbers below are **stylized round numbers**, chosen to show the mechanism. They are not real figures (Lesson 14 estimates those).

| Index | Index size | Tracking money | Slice |
|---|---:|---:|---:|
| Russell 1000 | $50tn | $1tn | 1 / 50 = 2% |
| Russell 2000 | $3tn | $0.3tn | 0.3 / 3 = 10% |

What each column means:

- **Index size** is the total tradable value of all members: every member's float-adjusted market cap added up. In the toy index this was the $19.4bn. The Russell 1000 is huge because it contains the largest US companies. The Russell 2000 has twice as many companies, but they are ranks 1,001–3,000, so every one is smaller than any Russell 1000 company. Market value is heavily concentrated at the top, so 2,000 small companies add up to far less than the 1,000 largest.
- **Tracking money** is the combined assets of all the index funds, ETFs, and institutional accounts that copy that index exactly. In the toy index this was the $1bn fund. In absolute dollars, less money tracks the Russell 2000 than the Russell 1000.
- **Slice** is tracking money ÷ index size: the fraction of each member's tradable shares that trackers own. It's the same calculation as the toy fund's 5.2%.

The key point is that **the slice depends on the ratio, not on the dollar amounts.** Less money tracks the Russell 2000, but the index is so much smaller that the money is a bigger fraction of it: 10% vs 2%.

Now follow one company, Z, with $6bn of tradable value, as it moves up from the Russell 2000 to the Russell 1000. Because of the band, this move only happens once Z has grown clearly past the cutoff, above the top of the band, not the first time it edges past rank 1,000.

**Step 1. What do Russell 2000 trackers hold today?** Their slice × Z's tradable value:

> 10% × $6bn = **$600m**

**Step 2. What will Russell 1000 trackers want after the move?**

> 2% × $6bn = **$120m**

**Step 3. Net trade.** Russell 2000 funds must sell all $600m, because Z is no longer in their index. Russell 1000 funds buy $120m.

> net passive flow = $120m − $600m = **−$480m**, a net sale of 8% of Z's tradable shares

**Check it a second way, through the weights.** Z's weight in the Russell 2000 is $6bn / $3tn = 0.2%. 0.2% × $0.3tn = $600m. Its weight in the Russell 1000 is $6bn / $50tn = 0.012%, and 0.012% × $1tn = $120m. That's the same answer.

In words: Z goes from being one of the biggest names in a small index (0.2% weight) to one of the smallest names in a huge index (0.012% weight). Its weight falls by a factor of about 17. The Russell 1000 has more money tracking it, but only about 3 times more, which is not enough to make up the difference. So the company gets bigger and index funds end up owning less of it. Moving down works in reverse and creates net buying. Chang, Hong, and Liskovich (2015) use exactly this cutoff to measure the price effect of index demand. Lesson 12 covers migrations in detail.

**The same dollar flow hits small caps harder.** Russell 2000 stocks trade far less each day than S&P 500 stocks, so a given amount of index buying is many more days of normal volume (Lesson 3). That fits Lesson 8's Petajisto numbers: the hidden index premium was larger for the Russell 2000 than for the S&P 500, even though the average price jump on an add was smaller.

**The S&P 500 is sticky, and Russell is rebuilt.** The S&P 500 holds a fixed number of companies, and a member is not removed just because it slips below an entry threshold. Changes happen one or a few at a time, usually when a seat opens. Russell rebuilds the whole list at each reconstitution, so hundreds of names can move in one day. One produces a steady trickle of single-stock events, and the other produces one or two very large basket trades each year.

**Profitability only matters for the S&P 500.** The S&P 500 requires positive earnings. Russell has no such test. A large, unprofitable company can sit in the Russell 1000 for years and become an S&P 500 candidate only once it posts positive earnings. That makes earnings releases a possible trigger for S&P inclusion.

| Difference | S&P 500 | Russell 1000 / 2000 |
|---|---|---|
| Moving up in size | Can lead to an add, which means buying | Crossing from the 2000 into the 1000 usually means net selling |
| Typical liquidity of affected stocks | Large, liquid | Many small, less liquid names in the 2000 |
| How changes arrive | A few names at a time, all year | Hundreds of names on reconstitution day |
| Profitability test | Yes | No |

### The S&P 500 entry checklist

Profitability is only one of the S&P 500's screens. Here is the full list from S&P's methodology (July 2026 version). A company has to pass **all** of them to become a *candidate*. Passing them doesn't mean it gets added; the committee still chooses.

| Rule | Requirement | Why it matters for flow |
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

## Price Return and Total Return

An index level built from prices alone is a **price return** index. It ignores dividends. A **total return** index assumes dividends are reinvested.

A stock at $100 pays a $2 dividend during the year and ends the year at $103. Its price return is 3%. Its total return is ($103 + $2 − $100) / $100 = 5%. An investor who held it earned 5%, not 3%.

This matters for tracking (Lesson 8). Index funds collect dividends, so they are normally compared with a total return version of their index. Comparing a fund with the price return index would make it look like it beat the index by the dividend yield. There is also a **net total return** version, which reinvests dividends after a standard withholding tax. It is used for funds that cannot reclaim taxes on foreign dividends.

## Common Misconceptions

A common mistake is to think that a bigger company always has a bigger weight. Weight follows *float-adjusted* market cap, so a company with a large strategic holder can have a smaller weight than a smaller company whose shares are widely held.

Another mistake is to think index providers buy stocks. S&P and FTSE Russell publish weights and calculate a number. The trading is done by the funds that copy the weights.

It is also tempting to think equal weighting is "more neutral." It is a different bet. It overweights smaller members relative to the market and creates predictable rebalance trades, whereas cap weighting mirrors the market and trades only when the recipe changes.

Finally, "the rules are public" does not mean every change is equally predictable. A mechanical ranking like Russell's can be recomputed by anyone, so the outcome is known, or nearly known, before the official list. A committee decision like the S&P 500's can only be given a probability until it is announced. For Russell, desks compete on running the ranking accurately and early. For S&P, they compete on judging probabilities and on reacting quickly to the announcement.

A related mistake is to treat rank day as an announcement. It is a measurement date. Nothing is published that day.

## Recap

An index is a recipe: eligibility rules choose the members, and a weighting rule sets each member's share. Most major equity indexes weight by float-adjusted market cap, which is price × shares outstanding × float factor. The float factor removes shares held by strategic owners who are unlikely to sell. That way the index asks only for shares that can actually be bought. A float-adjusted cap-weighted fund owns the same percentage of every member's float. That makes flow estimates simple: indexed money as a share of the index's total float cap tells you roughly what share of a new member's float must be bought. Price moves don't force cap-weighted funds to trade, but changes to membership, shares, or float do. Equal-weighted indexes trade on every scheduled rebalance. The S&P 500 uses committee discretion on top of published screens. The Russell indexes rank mechanically at two rebuilds a year, and that difference decides how far ahead a flow can be forecast. Russell's band lets current members stay in their index while they are inside a range around the cutoff ($2.7bn to $9.6bn in June 2026), so predicting Russell moves needs the current membership list as well as the ranking. Because index funds own a fixed share of each member's float, weight relative to the index matters more than absolute size. A company moving up from the Russell 2000 to the Russell 1000 can face net passive selling.

## New Terms

**eligibility rules**: The screens that decide which securities may join an index, such as size, liquidity, float, domicile, security type, and sometimes profitability.

**market capitalization (market cap)**: Share price times shares outstanding. The market value of all of a company's shares.

**shares outstanding**: The total number of a company's shares that have been issued and are held by anyone.

**free float**: The shares that ordinary investors can actually buy and sell, excluding strategic holdings.

**float factor / investable weight factor (IWF)**: The fraction of shares outstanding that an index counts as free float. IWF is S&P Dow Jones Indices' name for it.

**float-adjusted market cap**: Price × shares outstanding × float factor. Sometimes called investable market cap.

**market-cap weighting**: Weighting each member by its (usually float-adjusted) market cap divided by the index total.

**equal weighting**: Giving every member the same weight, which requires periodic rebalancing back to equal.

**size screen**: A rule that excludes companies below a minimum size, either a fixed threshold or a rank cutoff.

**liquidity screen**: A rule that excludes stocks that trade too little for funds to buy and sell at reasonable cost.

**rank day**: For the Russell indexes, the last business day of April, when eligible stocks are ranked by total market cap to set membership.

**mechanical ranking**: Setting membership by sorting companies on a published measure and applying fixed cutoffs, with no discretionary choice.

**preliminary list**: Russell's first published list of proposed additions and deletions, released a few weeks after rank day.

**lock-down period**: The stretch before Russell reconstitution day during which membership is treated as final.

**reconstitution**: A scheduled rebuild of an index's membership from scratch according to its rules. For Russell, twice a year: June (full) and December (additions and migrations).

**band**: A range around an index cutoff within which current members keep their index. New companies are judged by the cutoff alone.

**reconstitution day**: The day the new Russell membership takes effect, at the close. Index funds trade in that day's closing auction.

**quarterly rebalance**: For the S&P 500, the scheduled update after the close on the third Friday of March, June, September, and December.

**price return index**: An index calculated from prices only, ignoring dividends.

**total return index**: An index that assumes dividends are reinvested. The net version reinvests dividends after a standard withholding tax.

## Questions to Test Yourself

1. What determines a company's weight in a float-adjusted cap-weighted index?

Its float-adjusted market cap (price × shares × float factor) divided by the sum of all members' float-adjusted caps. Price, share count, and strategic ownership are the three inputs that can change it.

2. Why does free float matter?

It excludes shares that strategic holders won't sell, so the index only asks funds to buy shares that are actually available. Without it, index demand would compete for a pool of shares too small to supply it, and prices would be distorted.

3. How does market-cap weighting differ from equal weighting in the trades it causes?

Under cap weighting, holdings move with prices, so price changes alone never require a trade. Under equal weighting, price changes push holdings away from equal, so the fund must sell winners and buy losers at each scheduled rebalance.

4. A founder sells a large block and the stock's float factor rises. Why do index funds buy, and what do they sell?

The stock's float-adjusted cap and weight rise, so tracking funds must buy it. They pay for it by trimming every other member a little, because the weights must still add up to 100%.

5. Why are Russell changes easier to predict than S&P 500 changes?

Russell membership comes from a mechanical ranking on a known rank day, so anyone with the data can compute it. S&P 500 changes depend on committee choice among eligible candidates, so they can only be estimated as probabilities until S&P announces them.

6. A company grows and moves from the Russell 2000 to the Russell 1000. Why might passive funds be net sellers?

Trackers own a much bigger share of each member's float in the small index than in the big one, because the Russell 2000 is small relative to the money tracking it. The stock goes from a large weight in the Russell 2000 to a tiny weight in the Russell 1000, so Russell 2000 funds sell more than Russell 1000 funds buy.

## Sources

FTSE Russell. "Russell US Equity Indexes: Construction and Methodology." v7.2, August 2026. Section 6.10 (banding) and Appendix F (reconstitution schedule). [https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf](https://www.lseg.com/content/dam/ftse-russell/en_us/documents/ground-rules/russell-us-indexes-construction-and-methodology.pdf)

Yoshimoto, Catherine. "Russell Reconstitution June 2026: Larger Leaders, Stronger Small Caps." FTSE Russell Insights, June 16, 2026. [https://www.lseg.com/en/insights/ftse-russell/russell-reconstitution-june-2026-larger-leaders-stronger-small-caps](https://www.lseg.com/en/insights/ftse-russell/russell-reconstitution-june-2026-larger-leaders-stronger-small-caps)

New Street IR. "Russell Reconstitution Now Happens Twice a Year." October 14, 2026 (December 2026 dates). [https://newstreetir.com/2026/10/14/russell-reconstitution-now-happens-twice-a-year-what-does-that-mean-for-public-biotechs/](https://newstreetir.com/2026/10/14/russell-reconstitution-now-happens-twice-a-year-what-does-that-mean-for-public-biotechs/)

S&P Dow Jones Indices. "S&P U.S. Indices Methodology." July 2026. Eligibility Criteria (pp. 7–11), Index Construction (p. 12), Timing of Changes, and Index Committee sections. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)

Li, Kun, Xin (Kelly) Liu, and Shang-Jin Wei. 2021. "Is Stock Index Membership for Sale?" NBER Working Paper 29365. [https://www.nber.org/papers/w29365](https://www.nber.org/papers/w29365)

Sharfman, Bernard S., and Vincent Deluard. 2021. "Discretionary Decision-Making and the S&P 500 Index." CLS Blue Sky Blog, March 30, 2021. [https://clsbluesky.law.columbia.edu/2021/03/30/discretionary-decision-making-and-the-sp-500-index/](https://clsbluesky.law.columbia.edu/2021/03/30/discretionary-decision-making-and-the-sp-500-index/)

Agrawal, Vidhi, Eesha Khalid, Tianyu Tan, and Doris Xu. 2024. "Hunting Tomorrow's Leaders: Using Machine Learning to Forecast S&P 500 Additions & Removal." arXiv:2412.12539. [https://arxiv.org/abs/2412.12539](https://arxiv.org/abs/2412.12539)

Greenwood, Robin, and Marco Sammon. 2025. "The Disappearing Index Effect." *Journal of Finance* 80 (2): 657-698. [https://www.nber.org/system/files/working_papers/w30748/w30748.pdf](https://www.nber.org/system/files/working_papers/w30748/w30748.pdf)

Chang, Yen-Cheng, Harrison Hong, and Inessa Liskovich. 2015. "Regression Discontinuity and the Price Effects of Stock Market Indexing." *Review of Financial Studies* 28 (1): 212-246.

S&P Dow Jones Indices. "Float Adjustment Methodology." [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-float-adjustment.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-float-adjustment.pdf)

FTSE Russell (LSEG). "Four Decades of Russell Indexes Reconstitution." May 2, 2024. [https://www.lseg.com/en/ftse-russell/research/four-decades-russell-indexes-reconstitution](https://www.lseg.com/en/ftse-russell/research/four-decades-russell-indexes-reconstitution)

FTSE Russell (LSEG). "FTSE Russell Announces 2026 Russell US Indexes Reconstitution Schedule." Press release, March 2, 2026. [https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule](https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule)

CME Group. "Navigating the S&P 500 Rebalance: A Quarterly Market Ritual." 2025. [https://www.cmegroup.com/openmarkets/equity-index/2025/Navigating-the-S-P-500-Rebalance-A-Quarterly-Market-Ritual.html](https://www.cmegroup.com/openmarkets/equity-index/2025/Navigating-the-S-P-500-Rebalance-A-Quarterly-Market-Ritual.html)

FTSE Russell (LSEG). "Russell US Indexes: Moving to a Semi-Annual Index Reconstitution Frequency." December 17, 2025. [https://lseg.com/en/ftse-russell/research/russell-us-indexes-move-to-semi-annual-reconstitution](https://lseg.com/en/ftse-russell/research/russell-us-indexes-move-to-semi-annual-reconstitution)
