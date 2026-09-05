# Lesson 3: Liquidity, Spreads, Depth, and Market Impact

## Learning Goal

Lesson 2 showed how orders interact with books and venues. This lesson asks why large or urgent trades move prices, and how a flows desk should size that risk.

The core idea is that liquidity is the market's ability to absorb size without a large price concession. Volume is how much traded in the past. They are related, but they are not the same thing. Every meaningful flow should be compared to available liquidity, not only to market cap or yesterday's share count.

## The Problem: Size Meets Scarce Willingness

Suppose a passive fund must buy 2 million shares of XYZ by the close. The stock last traded at $100. Average daily volume is 10 million shares. The displayed ask shows a few thousand shares near $100.02.

The fund does not face a single price. It faces a supply curve. Nearby sellers may take a small amount. Larger size needs more sellers, higher prices, more time, or a dealer willing to warehouse risk. Price moves because someone has to be persuaded to take the other side.

```text
required buy size
  -> compare to depth, ADV, auction size
  -> urgency and predictability constrain how you trade
  -> liquidity providers demand compensation
  -> average fill moves away from arrival price
```

That compensation shows up as spread cost, impact, slippage, and benchmark shortfall.

## Quoted Liquidity Versus Realized Liquidity

Quoted liquidity is what the market advertises right now: the spread, displayed depth, and visible interest. Realized liquidity is what you actually get when you try to trade: fills, leftover size, and the price path your order creates.

A stock can look liquid on the quote screen and still be expensive to trade in size. Displayed depth can vanish when hit. Hidden and dark interest may or may not show up. A dealer who was willing to take 50,000 shares may refuse the next 500,000. For a flows desk, quoted liquidity is a starting estimate. Realized liquidity is the cost that hits PnL and tracking error.

## Spread, Depth, and Resiliency

The bid-ask spread is the immediate cost of crossing for small size. Wider spreads usually mean immediacy is more expensive.

Depth is how much size sits near those prices. Thin depth means a given order walks farther. Thick depth means the same order can finish closer to the touch.

Resiliency is how quickly liquidity replenishes after it is consumed. A resilient book refills. A fragile book stays hollow after a hit, so later slices of the same parent order pay more than the first slice suggested.

```text
spread     -> cost of a small immediate trade
depth      -> how far size must walk
resiliency -> whether liquidity comes back after you take it
```

All three matter for meta-orders, meaning large parent orders broken into many child orders over time. The first fill is not the whole cost story.

## A Small Worked Example

XYZ trades near $100. ADV, meaning average daily volume, is 10,000,000 shares: a typical day's traded share count, used as a rough liquidity screen. A fund must buy 2,000,000 shares. That is 20% of ADV if done in one day.

If the fund tries to buy too fast, it becomes a large share of what the market is naturally trading. Liquidity providers see persistent buy pressure, pull offers, or lean ahead. The fund's average buy price may rise from $100 toward $101 or further, depending on conditions. If instead the fund stretches the trade over several days, each day's participation is smaller, impact per day may fall, but the fund takes more price risk while unfinished and may miss a benchmark deadline.

A rough desk comparison starts with:

```text
shares_needed / ADV
shares_needed / expected auction volume
shares_needed / displayed depth near the touch
```

None of these is a complete cost model. Each asks the same practical question: how large is this flow relative to what the market can absorb?

## Why Urgency Raises Cost

Trading slowly usually reduces immediate impact because you take less of the market at once. Trading fast usually raises impact because you demand more liquidity per unit of time.

That is the classic execution tradeoff formalized in Almgren and Chriss (2001): faster trading increases impact cost; slower trading increases exposure to adverse price moves while the position is still open. A rebalance that must finish by the closing print has limited freedom. Completion risk and tracking-error risk can dominate the desire to be patient.

Urgency is not only a clock. It is also optionality. A discretionary buyer can walk away if price runs. A benchmark-sensitive buyer often cannot. Forced urgency is why index events can be expensive even when the "information" about the company is thin.

## Temporary Impact Versus Permanent Impact

Not every price move from trading lasts.

Temporary impact is the short-lived pressure from consuming liquidity. The book is hit, prices gap in your direction, then some of that move fades as liquidity returns or as opportunistic traders lean the other way.

Permanent impact is the part of the move that remains after the trade is done. In execution models, it is often treated as the lasting shift associated with the total quantity traded. In market terms, it can reflect inventory that must be held, beliefs that changed, or positioning that does not quickly reverse.

```text
temporary impact
  -> liquidity shock
  -> may fade after the flow finishes

permanent impact
  -> lasting reprice or lasting inventory transfer
  -> less likely to fully reverse
```

Holthausen, Leftwich, and Mayers documented temporary and permanent price effects around large-block trades decades ago. Almgren-Chriss later built optimal-execution mathematics around temporary and permanent impact components. For a flows desk, the useful question is crude but powerful: if this buy pressure ends at 4:00, how much of the move should reverse, and how much might stick because information, hedging, or positioning changed?

Lesson 4 separates information-driven moves from mechanical demand more carefully. Here the point is simpler: impact has a time profile, not just a size.

## Participation Rate, Slippage, and Implementation Shortfall

Participation rate is your trading rate relative to market volume over the execution window. Buying 200,000 shares in an hour when the stock trades 1,000,000 shares that hour is a 20% participation rate. High participation is easier to detect and usually more expensive.

Slippage is the difference between a reference price and the price you actually get. People use different references, so the word is slippery. Always ask: slippage versus what?

Implementation shortfall is a cleaner desk concept. It compares the decision or arrival price to the final execution outcome, including commissions and the cost of any unfilled residual marked at a closing or cancellation price. Perold popularized this way of measuring the true cost of trading, not just the commission line.

```text
arrival price = $100.00
average fill  = $100.40
shortfall     = 40 cents per share, before fees
```

That 40 cents mixes spread crossing, impact, timing, and adverse drift. The label "impact" alone is often too neat for what the tape actually did.

## Nonlinear Impact and Simple Scaling

Empirically, impact often rises less than one-for-one with size. A common regularity, sometimes called the square-root law, says that the average impact of a meta-order scales roughly like the square root of size relative to volume, scaled by volatility. Work associated with Bouchaud and others, and practitioner notes from firms such as CFM, treat this as an empirical pattern in normal conditions, not a physical constant.

That is a different point from "same shares, different speed." Taking 1,000 shares of displayed liquidity right now means walking the book. If only 300 shares sit at $100.02, then 400 at $100.03, then 300 at $100.05, your average is already above the touch, and you have emptied nearby depth. Working the same 1,000 shares over an hour as a meta-order — 100-share slices, some dark pings, some limit posts — usually costs less in impact because the book can refill between slices. You still have 1,000 shares of risk to transfer. You did not take 1,000 shares of *current* depth in one hit.

The square-root pattern is about comparing *sizes*, both worked the same way. Stylized: if 1,000 shares worked over the day costs about 10 basis points of impact, four times the size (4,000 shares) is not four times the cost. Square-root scaling would put it nearer 20 basis points, twice as much, not 40. That is square root, not log: log would be flatter still (nearer 12 basis points in this toy). A static book with equal depth on every tick would make 4× size cost about 4×. Perfect refill at the *same* price would make 4× size cost about the same. Markets sit between those. Same-price refill is the speed story above. The size story is a different refill: as the larger order pushes price, new sellers appear at worse prices, so the supply curve thickens. Extra size still costs more. It just does not cost linearly. Do not treat those numbers as a forecast.

Why a large order does not slip linearly: the displayed book is not the whole supply curve. Linear thinking assumes every tick has the same size, so four times the shares must walk four times as many ticks and the average fill is four times worse. That would be true if you were eating a frozen ladder. You are not. The first 1,000 shares take the cheap, nearby liquidity. The next 3,000 still push the price up, but each uptick recruits sellers who would not sell at $100.02 and who show up at $100.08 or $100.10: people who were waiting, hidden size, opportunistic offers. You need a higher price to clear 4,000 shares. You do not need four times the price move, because the ladder gets thicker as it rises. Slip of the parent order is an average across all those fills, so it rises with size, just much slower than one-for-one.

The practical implication is more important than the exact exponent. Doubling size does not simply double cost in a linear way, and tiny participation can look almost linear while larger participation becomes clearly costly. Comparing shares to ADV is a first screen. Thinking in participation rate and volatility is a better second screen. Full cost models belong later in the curriculum.

```text
rough screens
  Q / ADV
  participation rate during the window
  Q versus auction volume on event day
```

## Why Predictable Buyers Pay Before They Finish

If the market knows a large buyer must finish by a deadline, other traders can position ahead of that demand. Prices may rise before the forced buyer is done. The buyer then pays not only for the liquidity they personally consume, but for the anticipatory trading that crowded the path.

This is central to index-add and rebalance trading. Mechanical demand is estimable. Estimable demand attracts event traders, dealers, and hedge funds. Crowding can pull impact forward in time and leave more reversal risk after the forced flow ends.

```text
announced or inferred buy need
  -> anticipatory positioning
  -> price rises early
  -> forced buyer finishes at worse levels
  -> post-event fade if pressure was mostly temporary
```

## What Makes a Trade Easy or Hard

A trade is easier when size is small versus ADV and depth, urgency is low, direction is not widely anticipated, liquidity providers have balance-sheet room, and related hedges are cheap.

A trade is harder when size is large versus liquidity, the deadline is tight, many desks see the same flow coming, the name is already one-sided, volatility is high, or the only natural liquidity is concentrated in an auction.

Market cap is a weak substitute for these checks. A huge company can still be hard to trade on a specific day if event flow is large relative to that day's liquidity.

## Common Misconceptions

Volume is not liquidity. High volume can coexist with expensive immediacy if trading is one-sided, fleeting, or already spoken for by other urgent flow.

Paying the spread is not the whole cost of a large order. Impact, timing, and unfinished residuals often dominate.

If price rose while you bought, that does not prove the rise is permanent. Some of it may be temporary liquidity pressure that fades after you finish.

A low commission does not mean cheap execution. Implementation shortfall can be large while brokerage fees look tiny.

## Recap

Liquidity is willingness to take the other side without a large concession. Spreads price small immediacy, depth shapes how far size walks, and resiliency decides whether later slices stay cheap. Large or urgent orders create market impact because they demand scarce risk-bearing. Temporary impact may fade; permanent impact sticks. Participation rate, slippage versus a chosen benchmark, and implementation shortfall are the practical languages for measuring that cost. For flows trading, the first habit is always the same: compare the required trade to liquidity and to how predictable the demand is, not only to the stock's headline size.

## New Terms

**liquidity**: The ability to trade size without a large adverse price move. It depends on available counterparties, not just past volume.

**quoted liquidity**: Visible or advertised trading interest, such as spread and displayed depth.

**realized liquidity**: The liquidity actually obtained when trading, including fills, impact, and leftover risk.

**bid-ask spread**: The gap between best ask and best bid. Part of the cost of trading immediately in small size.

**depth**: Shares available at nearby price levels.

**resiliency**: How quickly quoted liquidity replenishes after it is taken.

**market impact**: The price movement caused by trading, especially by large or urgent orders.

**temporary impact**: The portion of impact that tends to fade after liquidity demand eases.

**permanent impact**: The portion of impact that remains after the trade is complete.

**participation rate**: Your traded volume as a fraction of market volume over the execution window.

**slippage**: The difference between a reference price and the achieved execution price. The reference must be specified.

**implementation shortfall**: The full cost of trading relative to an arrival or decision price, including impact, timing, fees, and residuals.

**average daily volume (ADV)**: A historical average of daily traded shares, used as a rough liquidity screen.

**meta-order**: A large parent order executed as many smaller child orders over time.

## Questions to Test Yourself

1. Why is volume not the same thing as liquidity?

Volume measures how much traded in a past window. Liquidity is about how much can trade now, at what price concession, and who will take the other side.

2. Why does urgency increase trading cost?

Faster trading demands more liquidity per unit of time, so impact usually rises. Slower trading can reduce impact but leaves more price risk while the order is open.

3. What makes a trade easy or hard to execute?

Ease rises when size is small versus depth and ADV, urgency is low, and the flow is not crowded. Hardness rises with size, deadlines, one-sided markets, volatility, and predictable competing demand.

4. Why can a predictable buyer push prices up before finishing?

Other traders can anticipate the forced demand and position ahead of it. The buyer then faces a path that has already moved against them.

5. What is the difference between temporary and permanent price impact?

Temporary impact is liquidity pressure that may fade after the flow ends. Permanent impact is the part of the move that remains because inventory, information, or positioning has changed.

6. If a stock is 20% of ADV to buy in one day, why is that a warning?

The fund would be a large share of that day's trading, so participation and detection risk are high. Impact and completion risk are likely much larger than the quoted spread suggests.
