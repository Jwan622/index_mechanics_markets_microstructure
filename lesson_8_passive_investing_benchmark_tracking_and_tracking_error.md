# Lesson 8: Passive Investing, Benchmark Tracking, and Tracking Error

## Learning Goal

Lesson 7 showed that a lot of flow piles into the closing auction because many funds are judged against the closing price. This lesson explains the funds behind that flow. An index fund has no opinion about the stocks it owns. Its only job is to match a benchmark. That job forces it to trade at set times and in set sizes, whether or not the price is attractive.

The key idea is that passive does not mean inactive. A fund that follows rules instead of views can still have to trade very large amounts. Because the rules are public, other traders can often predict those trades.

## The Problem: A Fund With No Opinion Still Has to Trade

An S&P 500 index fund holds $10 billion. The index committee announces that XYZ will join the index at the close on Friday with a weight of 0.20%. The fund now needs to own 0.20% × $10 billion = $20 million of XYZ by Friday's close.

The fund manager has not decided that XYZ is cheap. They may have no view at all. The fund buys because a rule changed. If it skipped the purchase, it would no longer hold what the index holds, and its returns would drift away from the index.

```text
index rule changes
  -> fund holdings no longer match the index
  -> fund must trade to match again
  -> trade happens near the index's effective time
```

That is the whole lesson in one picture. The rest explains how funds measure "match," why they cannot match perfectly, and why their trades matter to everyone else.

## An Index Is Not a Fund

These two are easy to mix up. An **index** is a list of stocks plus weights, and a set of rules for changing that list. S&P Dow Jones Indices publishes the S&P 500, but it does not own any S&P 500 stocks. Its "return" is a number calculated from closing prices. When S&P adds XYZ, nothing is bought. A line changes in a spreadsheet, and from the effective date's closing price onward the calculation includes XYZ.

An **index fund** is real money that copies the index. Index mutual funds and ETFs hold actual shares, so when the index adds XYZ they have to go into the market and buy it. When people say "the index buys XYZ," they mean the funds tracking it do.

The timeline matters for the rest of this lesson:

```text
announcement date      S&P says "XYZ joins at the close on Friday"
   |                   (the index has not changed yet; nobody is forced to buy yet)
   |   ... several trading days ...
   v
effective date close   the index starts using XYZ at Friday's closing price
                       index funds buy XYZ in Friday's closing auction
```

Index funds do not have to buy before the announcement, because they do not know about the change until then. They do not have to buy between the announcement and the effective date either. To match the index exactly, they buy at the same price the index uses, which is the effective-date close. Other traders who expect that demand often buy during the gap, which is where the price pressure comes from (see "Uninformed, but Still Important" below).

A **benchmark** is whichever index a fund is measured against. For an S&P 500 index fund and for an active large-cap manager, the benchmark is often the same: the S&P 500.

## Who Is Passive

A passive fund tries to deliver the return of an index instead of beating it. Most are index mutual funds or index ETFs. The amount of money involved is large. Cerulli Associates, citing Morningstar data, reported that passive US mutual funds and ETFs overtook active ones in total assets at the end of 2023. Each type held a little over $13 trillion.

Active funds are partly passive too. A large-cap active manager is usually measured against a benchmark such as the S&P 500. Holding a stock the benchmark owns at a lower weight is a bet, and so is skipping a stock the benchmark just added. So benchmark changes push active managers as well, even though they are not forced to follow them exactly.

## Tracking Difference and Tracking Error

To know how well a fund matches its index, compare their returns period by period. The difference is the fund's active return.

| Month | Fund return | Index return | Active return (fund − index) |
|---|---:|---:|---:|
| 1 | 1.02% | 1.00% | +0.02% |
| 2 | −0.53% | −0.50% | −0.03% |
| 3 | 2.01% | 2.00% | +0.01% |
| 4 | 0.46% | 0.50% | −0.04% |

Two numbers summarize this table. They answer different questions, so it helps to state the questions first.

- **Tracking difference** answers: *on average, did the fund beat or lag the index, and by how much?*
- **Tracking error** answers: *how predictable was the gap from month to month?*

### Tracking difference: the average gap

Add up the active returns and divide by the number of months:

```text
(+0.02) + (-0.03) + (+0.01) + (-0.04) = -0.04
-0.04 / 4 = -0.01% per month
```

On average the fund lagged by 0.01% a month. The sign matters. A negative tracking difference means investors got less than the index, and a positive one means they got more. Funds usually lag because they pay fees and the index does not, but some beat their index. The most common reason is income from lending their shares to short sellers, which the index does not earn.

### Tracking error: how much the gap wobbles

Tracking error is the standard deviation of the active returns. Standard deviation measures how far a set of numbers typically sits from its own average. Here is the calculation step by step.

**Step 1. Subtract the average from each month.** The average is −0.01, so add 0.01 to each active return:

| Month | Active return | Minus average (−0.01) | Deviation |
|---|---:|---|---:|
| 1 | +0.02 | +0.02 + 0.01 | +0.03 |
| 2 | −0.03 | −0.03 + 0.01 | −0.02 |
| 3 | +0.01 | +0.01 + 0.01 | +0.02 |
| 4 | −0.04 | −0.04 + 0.01 | −0.03 |

A deviation tells you how much that month missed the fund's *usual* gap, not how much it missed the index.

**Step 2. Square each deviation.** Squaring makes every value positive, so misses in opposite directions do not cancel. It also counts big misses more heavily than small ones.

```text
(+0.03)² = 0.0009
(-0.02)² = 0.0004
(+0.02)² = 0.0004
(-0.03)² = 0.0009
```

**Step 3. Add them up and divide by n − 1.**

```text
0.0009 + 0.0004 + 0.0004 + 0.0009 = 0.0026
0.0026 / (4 - 1) = 0.00087
```

This is the variance. We divide by 3 instead of 4 because the average was estimated from the same four numbers, which makes the deviations a bit smaller than they truly are. Dividing by n − 1 corrects for that. With many months of data, the difference hardly matters.

**Step 4. Take the square root.** Squaring left the variance in "percent squared," a unit with no intuitive meaning. The square root brings it back to percent:

```text
√0.00087 ≈ 0.029% per month
```

**Step 5. Annualize.** We have a monthly number, but people quote tracking error per year. The obvious guess is to multiply by 12. That would be wrong, because random misses partly cancel each other out.

Start with two months instead of twelve. Say each month's gap misses its average by either +0.03 or −0.03, like a coin flip, and the two months are independent. There are four equally likely outcomes for the two-month total:

| Month 1 | Month 2 | Two-month total |
|---:|---:|---:|
| +0.03 | +0.03 | +0.06 |
| +0.03 | −0.03 | 0.00 |
| −0.03 | +0.03 | 0.00 |
| −0.03 | −0.03 | −0.06 |

If the misses always went the same way, the two-month spread would be 0.06, which is 2 × 0.03. But half the time they cancel. So what is the typical size of the two-month total? Use the same standard-deviation recipe as before: square, average, then take the square root.

```text
squares:      0.0036, 0, 0, 0.0036
average:      0.0072 / 4 = 0.0018     (this is the two-month variance)
square root:  √0.0018 ≈ 0.042
```

The two-month standard deviation is about 0.042, not 0.06. Now look at the variance: 0.0018 = 2 × 0.0009. **Variances add up**: two months of independent misses give twice the monthly variance. Standard deviation is the square root of variance, so it grows with the square root of time:

```text
two-month standard deviation = √(2 × 0.0009) = √2 × 0.03 ≈ 0.042
```

The same logic works for twelve months. Add twelve monthly variances, then take the square root:

```text
annual variance            = 12 × monthly variance = 12 × 0.00087 = 0.0104
annual standard deviation  = √0.0104 ≈ 0.10% per year
```

That is the same as multiplying the monthly standard deviation by √12 ≈ 3.46: 0.029% × 3.46 ≈ 0.10%. The square root is not a trick. It comes from the fact that you add variances, then take one square root at the end.

This depends on the months being independent. If the fund tends to miss in the same direction month after month, for example during a long rally while holding cash, the misses don't cancel and the annual number is larger than √12 suggests. In the extreme case where every month misses the same way, it would be the full 12×. Compare this with tracking difference, which is an average return and does scale with time: lagging 0.01% a month means lagging about 0.12% a year.

```text
tracking difference   = average(fund return − index return)
tracking error        = standard deviation(fund return − index return)
annual tracking error ≈ monthly tracking error × √12
```

### Why the two numbers differ

Fund A lags its index by exactly 0.0025% every month. Its tracking difference is −0.0025% a month, which is a 0.03% fee spread over a year. Every deviation is zero, so its tracking error is zero. It is perfectly predictable.

Fund B is +0.20% one month and −0.20% the next. Its tracking difference is 0, but its tracking error is large. In any given month you cannot tell whether you will be ahead of or behind the index.

Investors care about both numbers. Tracking difference is the money they actually gain or lose against the index. Tracking error is the uncertainty around that. Index fund managers try hardest to keep tracking error small, because their product promises "the index return." A fund that is randomly 1% ahead one year and 1% behind the next is not delivering that, even when the misses average out. For an index fund, tracking error is a sign that the process is not under control, even if some of its misses happen to be favorable.

## Why a Fund Cannot Match Its Index Exactly

An index is a calculation, not a portfolio. It pays no fees, holds no cash, trades at exactly the closing price, and never pays a commission. A real fund does all of those things.

**Fees.** A fund that charges 0.03% a year starts 0.03% behind before anything else happens.

**Cash drag.** Funds hold some cash for redemptions and for dividends waiting to be reinvested. Suppose a fund is 98% in stocks and 2% in cash, and the index rises 10% in a year. The fund earns about 0.98 × 10% = 9.8%, plus a little interest on the cash. The 0.2% gap is cash drag. It reverses in a falling market. Many funds hold index futures against their cash to reduce it.

**Trading at a different time from the index.** The index assumes every change happens at the official closing price. Suppose a fund buys XYZ at 2:00 p.m. at $99.80 and XYZ then closes at $100.20. The fund paid 0.4% less than the index assumed, so on that trade it *beats* the index. The trouble is that it could just as easily have gone the other way. If XYZ had closed at $99.40, the fund would have paid 0.4% too much. Trading away from the close turns each index change into a small bet that can land in either direction. Those random wins and losses are exactly what tracking error measures. This is why so much index flow goes into the closing auction (Lesson 7). Buying at the close removes the bet.

**Not holding everything.** Some indexes are hard to hold in full. The US investment-grade bond index has thousands of bonds, many of which rarely trade. A small-cap index has illiquid names that are expensive to buy. Funds tracking those indexes often hold a subset, which is the subject of the next section.

**Smaller items.** Dividend timing, withholding taxes on foreign dividends, and income from lending shares to short sellers all move the fund's return slightly away from the index. Securities lending income can make a fund beat its index by a little.

## Full Replication, Sampling, and Optimization

There are three ways to build an index fund, and the choice trades tracking error against cost.

**Full replication** means holding every security in the index at its index weight. An S&P 500 fund can do this because all 500 stocks are liquid. Tracking error is low, but the fund must trade every name whenever the index changes, including the expensive ones.

**Representative sampling** means holding a subset chosen to look like the index on the features that drive returns. For a bond index, those features include sector, credit quality, and duration. iShares' AGG bond ETF does this. Its disclosure says the fund invests in "a representative sample of securities that collectively have an investment profile similar to that of the Underlying Index." The same disclosure says sampling "can be expected to produce a larger tracking error" than full replication. The fund accepts that in exchange for not buying thousands of illiquid bonds.

**Optimization** is sampling done with a risk model. The manager picks holdings that minimize the predicted tracking error for a given number of securities or a given trading budget. The result depends on the model. If the model's assumptions break, for example when a sector the model treated as stable suddenly moves, realized tracking error can be larger than predicted.

```text
full replication  -> lowest tracking error, highest trading burden
sampling          -> fewer holdings, more tracking error
optimization      -> fewest holdings for a target error, depends on the model
```

## Why Benchmark Tracking Creates Predictable Trades

Three facts about passive trading make it predictable.

The rules are public. Index providers publish their methodologies. Lessons 9 through 13 cover how they work, and Research Module 9a reads the actual S&P 500 and Russell rulebooks. Traders can often estimate index changes before they are announced, and they know them exactly once they are.

The timing is fixed. The index applies a change at a known effective date, usually at that day's close. A fund that wants zero tracking error trades in that closing auction, because that is the price the index uses.

The size can be estimated. Required dollars ≈ assets tracking the index × change in weight. "Assets tracking the index" means all the money set up to copy it exactly: index mutual funds, ETFs, and institutional accounts such as pension funds that hire a manager to replicate the index. Suppose that total is $500 billion and XYZ goes from not being in the index to a weight of 0.10%:

```text
$500,000,000,000 × 0.0010 = $500,000,000 of XYZ to buy
```

If XYZ normally trades $50 million a day, that is $500 million / $50 million = ten days of normal volume packed into one closing auction. (These are round numbers for illustration. Lesson 14 shows how desks estimate them.)

```text
public rules + fixed timing + estimable size
  -> traders can forecast the flow
  -> they can position before it, or offer to take the other side at the close
```

This is the core of a flows desk. Lesson 14 is about estimating this number carefully.

## Uninformed, but Still Important

Passive flow carries no information about a company's value. The fund buys XYZ because a rule says so, not because XYZ is cheap. In Lesson 6's terms, it is uninformed flow. A common mistake is to conclude that it therefore cannot move prices.

It moves prices because of size and timing, not information. Lesson 4 explained that demand for a stock is not perfectly flat. When a large buyer needs shares by a fixed time, sellers can ask for a higher price. Passive flow is large, one-sided, and on a known schedule, so it fits that description well.

The cost shows up in research. Petajisto (2011) studied S&P 500 and Russell 2000 changes from 1990 to 2005. From the announcement to the effective day, added stocks rose by an average of 8.8% in the S&P 500 and 4.7% in the Russell 2000. Deleted stocks fell by 15.1% and 4.6%. Index funds that wait to trade at the effective close buy after most of that move. Petajisto estimates the resulting hidden cost to index investors at a lower bound of 21 to 28 basis points a year for the S&P 500 and 38 to 77 basis points for the Russell 2000. A basis point is one hundredth of a percent, so 21 basis points is 0.21% and 77 is 0.77%. That is often more than the funds' stated fees. For comparison, large S&P 500 index funds charge only a few basis points.

**Why is the annual cost so much smaller than 8.8%?** The 8.8% is the overpayment on *one* stock. An index fund's whole portfolio does not turn over each year. In a typical year, only a small slice of the S&P 500's weight is in newly added stocks. The cost to the whole fund is roughly the premium times the share of the portfolio it applies to. Here is a stylized example (not Petajisto's exact method): if added stocks make up about 3% of the index's weight in a year and each one is bought about 8.8% too high, the cost is about 0.03 × 8.8% ≈ 0.26% of the fund per year. Deletions work the same way in reverse: the fund sells after the price has already fallen.

**Why is it called hidden?** The index uses the same inflated closing price as the fund. It "adds" XYZ at $100.20, the fund buys at $100.20, and their returns match. Tracking error is zero and tracking difference is unaffected. The cost is real, but it is built into the index return itself, so comparing the fund with its index will never show it. It appears only when you compare against a hypothetical fund that bought before the run-up. This is an important point: low tracking error proves the fund matched the index, not that the index's own trades were cheap.

This creates the central trade-off for an index fund:

```text
trade exactly at the effective close
  -> near-zero tracking error
  -> but pay whatever premium others have built in

trade earlier or spread the trade out
  -> may avoid some of the premium
  -> but take on tracking error
```

Neither choice is free. A fund's mandate and how its investors judge it decide which cost it prefers.

## Benchmarked Active Funds and Closet Indexing

Tracking error also describes active funds, but here the funds want some of it. A manager with zero tracking error is just an expensive index fund.

Tracking error alone does not tell you how active a manager is. Cremers and Petajisto (2009) proposed active share: the percentage of a fund's holdings that differs from its benchmark's holdings. A fund that owns exactly the benchmark has an active share of 0%. A fund with no overlap has an active share of 100%. Tracking error, which is based on returns, picks up bets on broad factors such as sector or size. Active share, which is based on holdings, picks up stock selection. A fund with low active share and low tracking error is often called a closet indexer. It markets itself as active and charges active fees, but its portfolio looks almost exactly like its benchmark.

Why does that matter to a flows desk? Take an active fund benchmarked to the S&P 500 that holds 480 of the 500 stocks at close to index weights. When S&P adds XYZ, the fund does not *have* to buy it. But not owning XYZ would be a bet against a stock that its benchmark now holds, and that bet would raise its tracking error, which is something a closet indexer tries to avoid. So it usually buys XYZ too, often around the same date. Its trades then look a lot like an index fund's. When a desk estimates the demand from an index change, the forced buying from index funds is the floor. Closet indexers and other benchmark-hugging active funds can add to it.

## Common Misconceptions

A common mistake is to think passive means inactive. Passive funds trade every time the index changes, every time money flows in or out, and every time dividends need reinvesting. The trades are rule-based, not rare.

Low tracking error does not mean good returns. A fund can track its index closely while losing its fee every year, and the index itself can overpay for additions. Tracking difference measures how much investors gain or lose relative to the index. It is usually a small loss, but it can be a gain. Tracking error measures how predictable that gap is.

Uninformed does not mean harmless. Passive flow tells you nothing about a company's value, but large, predictable, deadline-driven demand still moves prices. Others can position ahead of it.

Zero tracking error is not always the right goal. Driving tracking error to zero can mean paying the full index premium at the close. Some funds accept a small tracking error to trade more cheaply.

## Recap

An index is a calculation. An index fund is the real money that has to trade to copy it. A passive fund buys and sells to keep its holdings matched to an index, not because it has a view on value. How well it matches is measured by tracking difference, the average gap to the index (which can be negative or positive), and by tracking error, the standard deviation of that gap. Fees, cash drag, trading at times other than the index's close, and holding a sample instead of the whole index all keep a fund from matching perfectly. Full replication, sampling, and optimization trade a lower tracking error against a lower trading cost. Because index rules are public, timing is fixed, and sizes can be estimated, passive trades are predictable. That predictability lets other traders position ahead of the flow or supply liquidity into it. It is also why the flow moves prices even though it carries no information.

## New Terms

**index**: A published list of securities and weights, plus rules for changing them. It is a calculation, not a portfolio, and it holds no money.

**index fund**: A mutual fund or ETF holding real securities chosen to copy an index's return. It must actually trade when the index changes.

**passive fund**: A fund that tries to match the return of an index rather than beat it. Index funds are passive funds.

**benchmark**: The index a fund is measured against, whether the fund is passive or active.

**announcement date**: The day an index provider makes a change public.

**effective date**: The day the change takes effect in the index, usually at that day's closing price.

**active return**: The fund's return minus its benchmark's return over the same period.

**tracking difference**: The average active return over a period. Negative means the fund lagged the index and positive means it beat it. For an index fund it is usually close to minus the fee.

**standard deviation**: The typical distance of a set of numbers from their average: the square root of the average squared deviation.

**tracking error**: The standard deviation of active returns. It measures how predictable the fund's gap to its benchmark is, not whether the gap is good or bad.

**basis point (bp)**: One hundredth of a percent. 1 bp = 0.01%, so 38 bp = 0.38%.

**cash drag**: The gap between a fund's return and its index's return caused by holding cash that the index does not hold.

**full replication**: Holding every index security at its index weight.

**representative sampling**: Holding a subset of index securities chosen to match the index's main characteristics.

**optimization**: Choosing a subset of holdings with a risk model to minimize predicted tracking error.

**active share**: The percentage of a fund's holdings that differs from its benchmark's holdings.

**closet indexer**: A fund sold as active, with active fees, whose holdings and returns stay close to its benchmark. Its trades around index changes often look like an index fund's.

**index premium**: The extra price paid for a stock because index funds must buy it at a fixed time.

## Questions to Test Yourself

1. Why does an index fund buy or sell without a view on valuation?

Its job is to hold what the index holds, so it trades whenever the index rules change or money comes in or out. Whether the stock is cheap does not enter the decision.

2. What is tracking error?

It is the standard deviation of the difference between the fund's return and the index's return. It measures how consistently the fund follows the index, while tracking difference measures how far behind it falls on average.

3. Why does benchmark tracking create predictable trades?

Index rules are public, changes take effect at a known close, and the required size is roughly assets tracking the index times the weight change. Anyone who does that arithmetic can forecast the flow.

4. Why are passive flows important even if they are not informed?

They are large, one-sided, and on a deadline, so they need someone to take the other side at a price concession. That moves prices and creates a hidden cost for index investors even with no information involved.

5. Why might a fund not perfectly replicate its benchmark?

Some indexes contain thousands of illiquid securities that are expensive to buy, so the fund holds a representative sample instead. Fees, cash, and trading at prices other than the index's close add further gaps.

## Sources

Cerulli Associates. "The Battle of Passive vs. Active Reaches New Milestone." [https://cerulli.com/press-releases/the-battle-of-passive-vs.-active-reaches-new-milestone](https://cerulli.com/press-releases/the-battle-of-passive-vs.-active-reaches-new-milestone)

BofA Finance LLC. Form 424B2, describing the iShares Core U.S. Aggregate Bond ETF's representative sampling strategy. [https://www.sec.gov/Archives/edgar/data/1682472/000148105723009130/form424b2.htm](https://www.sec.gov/Archives/edgar/data/1682472/000148105723009130/form424b2.htm)

Petajisto, Antti. 2011. "The Index Premium and Its Hidden Cost for Index Funds." *Journal of Empirical Finance* 18 (2): 271-288. [https://ww.petajisto.net/papers/petajisto%202011%20jef%20-%20hidden%20cost%20for%20index%20funds.pdf](https://ww.petajisto.net/papers/petajisto%202011%20jef%20-%20hidden%20cost%20for%20index%20funds.pdf)

Cremers, K. J. Martijn, and Antti Petajisto. 2009. "How Active Is Your Fund Manager? A New Measure That Predicts Performance." *Review of Financial Studies* 22 (9): 3329-3365.
