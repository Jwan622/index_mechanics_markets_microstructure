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

| Question | Answer | Same for every stock? |
|---|---|---|
| How much of the *fund's money* is in this stock? | the weight (51.5%, 20.6%, 27.8%) | No |
| How much of *this company's tradable shares* does the fund own? | 5.2% | Yes |

### Why the slice is the same for every stock

Take A. The fund puts A's share of the index into A:

```text
dollars in A = (A's tradable value / total tradable value) × fund size
             = ($10.0bn / $19.4bn) × $1bn
```

To see what fraction of A's tradable value the fund owns, divide by A's tradable value ($10.0bn). The $10.0bn appears on the top and the bottom, so it cancels:

```text
fraction of A owned = dollars in A / $10.0bn
                    = $1bn / $19.4bn
                    = 5.2%
```

The same cancellation happens for B and C. Each stock's own size drops out, and what is left is always the same ratio: **fund size ÷ total tradable value of the index**. A big stock gets more dollars, but it also has more shares to buy. Weighting by tradable value scales the dollars to match exactly.

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

| Stock | Weight before | Weight after | Fund owns of its tradable shares |
|---|---:|---:|---:|
| A | 51.5% | 46.7% | 5.2% → 4.7% |
| B | 20.6% | 18.7% | 5.2% → 4.7% |
| C | 27.8% | 25.2% | 5.2% → 4.7% |
| D | — | 9.3% | 0% → 4.7% |
| **Total** | 100% | 100% | | Lesson 14 refines this estimate with real indexed-asset numbers, but the logic is exactly this.

## Why Cap Weighting Rarely Forces Trades and Equal Weighting Often Does

Suppose stock A rises 10% tomorrow and nothing else moves. In a cap-weighted index, A's weight rises because its market cap rose. The fund's A shares also rose 10%, so its holdings already match the new weights. **The fund does not need to trade.** Price moves rebalance a cap-weighted portfolio automatically.

An **equal-weighted index** gives every member the same weight, here 33.3% each, regardless of size. After A rises 10%, the fund's A position is now more than one third of the portfolio. To get back to equal weights, the fund must sell some A and buy B and C. Equal-weighted indexes therefore rebalance on a fixed schedule; the S&P 500 Equal Weight Index, for example, resets to equal weights each quarter. Every rebalance date is a predictable trade, which sells recent winners and buys recent losers.

| Weighting scheme | When prices move | Result |
|---|---|---|
| Cap weighting | holdings and target weights move together | no trade needed |
| Equal weighting | holdings drift away from equal | trade at each scheduled rebalance |

The three schemes give very different portfolios from the same three stocks:

| Stock | Float-adjusted cap weight | Total cap weight | Equal weight |
|---|---:|---:|---:|
| A | 51.5% | 38.5% | 33.3% |
| B | 20.6% | 38.5% | 33.3% |
| C | 27.8% | 23.1% | 33.3% |

A common mistake is to think cap-weighted index funds never trade. They trade whenever something other than price changes the recipe: membership changes, share issuance or buybacks, float changes, and the corporate actions covered in Lesson 10.

## When the Recipe Changes, Funds Trade

Return to the $1 billion fund. The founder of B sells half of their stake in a public offering, so B's float factor rises from 0.40 to 0.70. Prices don't change.

B's float-adjusted cap becomes $10.0bn × 0.70 = $7.0bn, so the new total is 10.0 + 7.0 + 5.4 = $22.4bn.

| Stock | Old weight | New weight | Old holding | New holding | Trade |
|---|---:|---:|---:|---:|---|
| A | 51.5% | 44.6% | $515m | $446m | sell $69m |
| B | 20.6% | 31.3% | $206m | $313m | **buy $106m** |
| C | 27.8% | 24.1% | $278m | $241m | sell $37m |

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

A tiny version: suppose there were only five eligible companies and the "large-cap" index took the top two.

| Company | Price on rank day | Shares outstanding | Total market cap | Rank | Index |
|---|---:|---:|---:|---:|---|
| P | $80 | 500m | $40bn | 1 | large-cap |
| Q | $25 | 1,200m | $30bn | 2 | large-cap |
| R | $60 | 400m | $24bn | 3 | small-cap |
| S | $10 | 2,000m | $20bn | 4 | small-cap |
| T | $45 | 300m | $13.5bn | 5 | small-cap |

If R had closed at $80 on rank day instead of $60, its cap would be $32bn. It would rank second, move into the large-cap index, and push Q down. The rank-day closing price decides membership. (The real rules also have a band around the cutoff, so a stock near the line doesn't jump back and forth every year. Lesson 9a covers that detail.)

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

So, to answer the obvious question directly: Russell does *not* announce additions on the last day of April. That day is when the *measurement* happens. The first official list comes about three weeks later, and the trade happens about two months later. In the past this happened once a year in June. Starting in December 2026, FTSE Russell will also run a December reconstitution, using a schedule it publishes separately.

**S&P 500:**

| Timing | Event | What it means |
|---|---|---|
| No fixed date | **Committee decision** | The committee picks additions from eligible candidates, often to replace a company leaving the index after an acquisition. |
| Days to a couple of weeks before the effective date | **Announcement** | S&P publishes the change, usually after the close. This is the first time the market knows for sure. |
| After the close on the third Friday of March, June, September, and December | **Quarterly rebalance** | Scheduled changes and share-count updates take effect. Index funds trade in that day's closing auction. |
| Any date | **Off-cycle change** | A merger, acquisition, or bankruptcy can trigger a replacement outside the quarterly schedule. |

### Why one is forecastable and the other isn't

Russell's rule is mechanical, so it *can* be computed in advance. As soon as rank day closes, a trader with price and share-count data can sort the companies and get very close to the preliminary list, three weeks before FTSE Russell publishes it. Even before rank day, they can estimate it, with uncertainty only about how prices will move before April 30. That is why Russell flow is crowded early. Many desks are running the same sort.

The S&P 500 is different. Being eligible (large enough, profitable, liquid, enough float) only makes a company a *candidate*. The committee then chooses among candidates, considering things like sector balance, and often acts only when a seat opens up. Traders can rank candidates by how likely they are to be picked, but they cannot know who is added until S&P announces. So for S&P, the main price move tends to come on the announcement. For Russell, much of it can come before the official list.

### Other differences that matter for flow

The table above covers the rules. Four more differences change how the flow behaves.

**Moving *up* from the Russell 2000 can mean being *sold*.** This is the most counterintuitive one. Use the rule from the toy index: a cap-weighted fund owns the same share of every member's float, equal to the money tracking the index divided by the index's total float cap. Here are stylized round numbers, chosen only to show the mechanism:

| Index | Total float cap | Money tracking it | Share of each member's float owned by trackers |
|---|---:|---:|---:|
| Russell 1000 | $50tn | $1tn | 1 / 50 = 2% |
| Russell 2000 | $3tn | $0.3tn | 0.3 / 3 = 10% |

A company that grows and moves from the Russell 2000 into the Russell 1000 leaves an index where trackers hold about 10% of its float. It joins one where trackers hold about 2%. Russell 2000 funds sell everything they hold, Russell 1000 funds buy a smaller amount, and the net passive flow is a *sale* of about 8% of the float. The reason is that the stock goes from being one of the largest names in a small index to one of the smallest names in a big index. Its weight falls even though the company got bigger. Moving down works in reverse and creates net buying. Chang, Hong, and Liskovich (2015) use exactly this cutoff to measure the price effect of index demand. Lesson 12 covers migrations in detail.

**The same dollar flow hits small caps harder.** Russell 2000 stocks trade far less each day than S&P 500 stocks, so a given amount of index buying is many more days of normal volume (Lesson 3). That fits Lesson 8's Petajisto numbers: the hidden index premium was larger for the Russell 2000 than for the S&P 500, even though the average price jump on an add was smaller.

**The S&P 500 is sticky, and Russell is rebuilt.** The S&P 500 holds a fixed number of companies, and a member is not removed just because it slips below an entry threshold. Changes happen one or a few at a time, usually when a seat opens. Russell rebuilds the whole list at each reconstitution, so hundreds of names can move in one day. One produces a steady trickle of single-stock events, and the other produces one or two very large basket trades each year.

**Profitability only matters for the S&P 500.** The S&P 500 requires positive earnings. Russell has no such test. A large, unprofitable company can sit in the Russell 1000 for years and become an S&P 500 candidate only once it posts positive earnings. That makes earnings releases a possible trigger for S&P inclusion.

| Difference | S&P 500 | Russell 1000 / 2000 |
|---|---|---|
| Moving up in size | Can lead to an add, which means buying | Crossing from the 2000 into the 1000 usually means net selling |
| Typical liquidity of affected stocks | Large, liquid | Many small, less liquid names in the 2000 |
| How changes arrive | A few names at a time, all year | Hundreds of names on reconstitution day |
| Profitability test | Yes | No |

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

An index is a recipe: eligibility rules choose the members, and a weighting rule sets each member's share. Most major equity indexes weight by float-adjusted market cap, which is price × shares outstanding × float factor. The float factor removes shares held by strategic owners who are unlikely to sell. That way the index asks only for shares that can actually be bought. A float-adjusted cap-weighted fund owns the same percentage of every member's float. That makes flow estimates simple: indexed money as a share of the index's total float cap tells you roughly what share of a new member's float must be bought. Price moves don't force cap-weighted funds to trade, but changes to membership, shares, or float do. Equal-weighted indexes trade on every scheduled rebalance. The S&P 500 uses committee discretion on top of published screens. The Russell indexes rank mechanically, and that difference decides how far ahead a flow can be forecast. Because index funds own a fixed share of each member's float, weight relative to the index matters more than absolute size. A company moving up from the Russell 2000 to the Russell 1000 can face net passive selling.

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

**reconstitution**: A scheduled rebuild of an index's membership from scratch according to its rules.

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

Chang, Yen-Cheng, Harrison Hong, and Inessa Liskovich. 2015. "Regression Discontinuity and the Price Effects of Stock Market Indexing." *Review of Financial Studies* 28 (1): 212-246.

S&P Dow Jones Indices. "S&P U.S. Indices Methodology." [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-us-indices.pdf)

S&P Dow Jones Indices. "Float Adjustment Methodology." [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-float-adjustment.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-float-adjustment.pdf)

FTSE Russell (LSEG). "Four Decades of Russell Indexes Reconstitution." May 2, 2024. [https://www.lseg.com/en/ftse-russell/research/four-decades-russell-indexes-reconstitution](https://www.lseg.com/en/ftse-russell/research/four-decades-russell-indexes-reconstitution)

FTSE Russell (LSEG). "FTSE Russell Announces 2026 Russell US Indexes Reconstitution Schedule." Press release, March 2, 2026. [https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule](https://lseg.com/en/media-centre/press-releases/ftse-russell/2026/russell-reconstitution-2026-schedule)

CME Group. "Navigating the S&P 500 Rebalance: A Quarterly Market Ritual." 2025. [https://www.cmegroup.com/openmarkets/equity-index/2025/Navigating-the-S-P-500-Rebalance-A-Quarterly-Market-Ritual.html](https://www.cmegroup.com/openmarkets/equity-index/2025/Navigating-the-S-P-500-Rebalance-A-Quarterly-Market-Ritual.html)

FTSE Russell (LSEG). "Russell US Indexes: Moving to a Semi-Annual Index Reconstitution Frequency." December 17, 2025. [https://lseg.com/en/ftse-russell/research/russell-us-indexes-move-to-semi-annual-reconstitution](https://lseg.com/en/ftse-russell/research/russell-us-indexes-move-to-semi-annual-reconstitution)
