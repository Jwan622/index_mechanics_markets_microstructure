# Lesson 10: Index Divisors, Corporate Actions, and Continuity

## Learning Goal

An index level like "S&P 500 at 6,000" is meant to answer one question: *how much have prices moved?* But the stocks inside the index keep changing. Companies are added and removed, they issue shares, split their stock, pay dividends, and spin off divisions. Each of these changes the index's total market value even when no price moved. This lesson explains the **divisor**, the number index providers adjust so that only price moves change the index level. It then goes through the common corporate actions one at a time.

The desk-relevant point is a distinction that is easy to blur. Some events change the divisor. Some events force index funds to trade. These are **two different questions with two different tests**, and the answers don't always match. A stock split changes neither. A share issuance changes both. A spin-off doesn't change the divisor on the day it happens, but it creates a forced sale later. Knowing which is which tells you where the flow is.

## The Problem: A Sum of Values Jumps for the Wrong Reasons

Use Lesson 9's three-stock toy index. Nothing has changed from Lesson 9:

| Stock | Price | Tradable shares | Tradable value |
|---|---:|---:|---:|
| A | $50 | 200m | $10.0bn |
| B | $100 | 40m | $4.0bn |
| C | $20 | 270m | $5.4bn |
| **Total** | | | **$19.4bn** |

(Tradable shares = shares outstanding × float factor, from Lesson 9: 200m × 1.00, 100m × 0.40, 300m × 0.90.)

The simplest possible "index" is just the total, $19.4bn. Now suppose the index adds stock D (also from Lesson 9: $40, 50m tradable shares, $2.0bn of tradable value) overnight, and no price moves.

> total before = $19.4bn
> total after = $19.4bn + $2.0bn = $21.4bn

The total rose 10.3%. But no stock went up, and nobody who held these stocks made any money. The jump came only from the list getting longer. A number that rises 10.3% when nothing happened is useless for measuring returns.

## The Fix: Divide by a Number You Can Adjust

Index providers publish

> **index level = total tradable value of the members ÷ divisor**

The **divisor** is a scaling number chosen by the index provider. It has no economic meaning by itself. It is not a share count and not a price. It does two jobs:

1. **Scaling.** It turns a total measured in trillions into a readable number. S&P's Index Mathematics Methodology gives the example of a $20 trillion total and a $10 billion divisor, which gives a level of 2,000.
2. **Continuity.** Whenever the total changes for a reason other than price, the provider changes the divisor by the same proportion, so the level doesn't jump.

### Step 1. Set the starting divisor

Say the toy index starts at a level of 1,000. The starting level is a free choice: providers pick a round **base value** on a **base date**, and from then on only percentage changes matter. The divisor must be whatever makes that starting level true:

> divisor = total ÷ level = $19.4bn ÷ 1,000 = **$19.4m**

Check: $19.4bn ÷ $19.4m = 1,000.

### Step 2. A price move changes the level (as it should)

A rises 10%, from $50 to $55. Nothing else changes, and the divisor stays at $19.4m.

> A's new value = 200m × $55 = $11.0bn
> new total = $11.0bn + $4.0bn + $5.4bn = $20.4bn
> new level = $20.4bn ÷ $19.4m = **1,051.5**

The index rose 5.15%. **A second way to check it:** the index return should be the weighted average of member returns. A's weight was 51.5% (Lesson 9), and the other stocks returned 0%:

> 51.5% × 10% + 20.6% × 0% + 27.8% × 0% = **5.15%**

Both routes agree. When the divisor stays fixed, the level moves exactly with prices.

### Step 3. Adding a stock changes the divisor, not the level

Go back to the starting point (level 1,000, divisor $19.4m) and add D overnight.

**Without adjusting:** $21.4bn ÷ $19.4m = 1,103.1, a fake 10.3% jump.

**With adjusting:** choose a new divisor that keeps the level at 1,000 with the new total:

> new divisor = new total ÷ old level = $21.4bn ÷ 1,000 = **$21.4m**

Check: $21.4bn ÷ $21.4m = 1,000. The level opens where it closed.

S&P's Index Mathematics Methodology writes the same adjustment in an equivalent "additive" form. The change in the divisor is the change in market value divided by the index level:

> new divisor = old divisor + (change in value ÷ level) = $19.4m + ($2.0bn ÷ 1,000) = $19.4m + $2.0m = **$21.4m**

Both forms give $21.4m. The additive form is handy because each change, whether an add, a delete, or a share update, contributes its own piece, and the pieces can be summed.

### Step 4. Confirm the new divisor measures returns correctly

The next day, every stock rises 1%:

> new total = $21.4bn × 1.01 = $21.614bn
> level = $21.614bn ÷ $21.4m = **1,010**

That's up exactly 1% from 1,000. The new divisor keeps measuring price moves correctly with D included.

### The rule in one sentence

S&P's methodology states it directly: any change that alters the index's total market value *while prices are held constant* requires a divisor adjustment. Price moves change the level. Everything else changes the divisor.

```text
price moves                      -> total changes -> level changes      (divisor fixed)
membership, shares, float, etc.  -> total changes -> divisor changes    (level fixed)
```

## The Second Question: Do Index Funds Have to Trade?

The divisor is bookkeeping for the index. Index funds don't hold the divisor; they hold shares. So "does the divisor change?" says nothing directly about flow. The test for flow is different:

> **A fund must trade when its target holdings change in a way its current holdings don't follow automatically.**

Lesson 9 already showed the two basic cases. When A's price rises 10%, the fund's A shares rise 10% too, so its holdings still match the new weights and **no trade is needed**. When B's float factor rises, B's weight rises but the fund's B shares don't change, so it **must buy B**. Every corporate action below gets both tests: (1) does the divisor change, and (2) do funds trade?

Each example starts from the same base: the toy index at level 1,000 with a $19.4m divisor, and Lesson 9's $1 billion fund holding

| Stock | Weight | Dollars held | Shares held |
|---|---:|---:|---:|
| A | 51.5% | $515.5m | 10.31m |
| B | 20.6% | $206.2m | 2.062m |
| C | 27.8% | $278.4m | 13.92m |

(From Lesson 9: weight × $1bn, then ÷ price. The fund owns 5.155% of every stock's tradable shares, which is $1bn ÷ $19.4bn.)

## Corporate Action 1: Stock Split

A does a 2-for-1 split: every A share becomes two shares, and the price halves.

| | Before | After |
|---|---:|---:|
| A price | $50 | $25 |
| A tradable shares | 200m | 400m |
| A tradable value | $10.0bn | $10.0bn |

**Divisor?** The total is unchanged at $19.4bn, so **no divisor change**. S&P's Policies & Practices document lists splits as "no divisor adjustment."

**Fund trade?** The fund's 10.31m A shares become 20.62m shares at $25, which is still $515.5m. Its holdings follow automatically, so **no trade**.

A split is a change of units, like re-pricing a pizza by the slice instead of by the half. Nothing about the value or the weights changes.

## Corporate Action 2: Share Issuance

C sells 30m new shares to the public at $20, raising $600m. All the new shares are tradable.

**Step 1. C's new tradable shares and value.**

> tradable shares = 270m + 30m = 300m
> tradable value = 300m × $20 = **$6.0bn** (was $5.4bn)

**Step 2. New total and divisor.**

> new total = $10.0bn + $4.0bn + $6.0bn = **$20.0bn**
> new divisor = $20.0bn ÷ 1,000 = **$20.0m**

Prices didn't move, the total did, so **the divisor changes** and the level stays at 1,000.

**Step 3. What must the fund hold now?** C's new weight is $6.0bn ÷ $20.0bn = 30.0%.

> C target = 30.0% × $1,000m = $300.0m
> C held = $278.4m
> **buy C ≈ $21.6m** (about 1.08m shares at $20)

**Step 4. Where does the money come from?** A and B didn't change, but the total grew, so their weights fell:

| Stock | New weight | Target | Held | Trade |
|---|---:|---:|---:|---|
| A | 10.0 / 20.0 = 50.0% | $500.0m | $515.5m | sell $15.5m |
| B | 4.0 / 20.0 = 20.0% | $200.0m | $206.2m | sell $6.2m |
| C | 6.0 / 20.0 = 30.0% | $300.0m | $278.4m | buy $21.6m |

The sales ($15.5m + $6.2m = $21.7m, with rounding) pay for the purchase.

**A second way to check it.** The fund's slice of every company falls from $1bn ÷ $19.4bn = 5.155% to $1bn ÷ $20.0bn = 5.0%. C now has 300m tradable shares:

> 5.0% × 300m = 15.0m shares, versus 13.92m held → buy **1.08m shares** ($21.6m)

Same answer.

**When does this happen?** That depends on the rulebook. S&P's Policies & Practices document puts an offering on an *accelerated* track if it is at least $150 million **and** at least 5% of the shares before the offering. In that case S&P gives at least one business day's notice for US stocks. C's offering qualifies on both counts:

> $600m ≥ $150m, and 30m ÷ 300m = 10% ≥ 5%

So index funds would buy C within days. A smaller issuance waits for the quarterly share update, after the close on the third Friday of March, June, September, or December. Lesson 11 shows how this kind of timing clause changes when the flow arrives.

A **buyback** is the mirror image: fewer shares, a lower tradable value, a smaller divisor, and **funds sell** the stock to match.

## Corporate Action 3: Ordinary Dividend

A pays its regular dividend of $1 a share. On the **ex-dividend date** (the first day the stock trades without the right to that dividend), assume A's price drops by exactly the dividend, from $50 to $49, and nothing else moves. That is a simplifying assumption. Real prices move for other reasons on the same day.

**Divisor?** S&P's rule for ordinary cash dividends is to adjust neither the price nor the shares, so **no divisor change**. The price index simply falls:

> A's value = 200m × $49 = $9.8bn
> new total = $9.8bn + $4.0bn + $5.4bn = $19.2bn
> price index level = $19.2bn ÷ $19.4m = **989.7** (down 1.03%)

That 1.03% drop is not a loss to investors. They received the dollar in cash. This is why Lesson 9 said funds are compared with the **total return** index, which puts the dividend back.

**How the total return index puts it back.** S&P's Index Mathematics Methodology converts the dividend into index points:

**Step 1. Total dividend paid by index members today.**

> $1 × 200m index shares of A = $200m

**Step 2. Convert to index points by dividing by the price index's divisor.**

> $200m ÷ $19.4m = **10.31 points**

**Step 3. Total return for the day = (price level + dividend points) ÷ yesterday's price level.**

> (989.7 + 10.31) ÷ 1,000 = 1.0000 → **0.00%**

The total return index doesn't move. The price drop and the dividend cancel, which is right, since investors are no better or worse off.

**Fund trade?** The fund receives $1 × 10.31m shares = **$10.3m in cash**. Its total value is unchanged:

> A: 10.31m × $49 = $505.2m, B $206.2m, C $278.4m, cash $10.3m → total **$1,000m**

But cash isn't in the index, so to keep tracking (Lesson 8's cash drag), the fund reinvests it. S&P's methodology says total return indexes reinvest dividends across the whole index, not in the stock that paid them. The fund therefore buys a little of everything at the new weights:

| Stock | New weight | Target | Held | Buy |
|---|---:|---:|---:|---:|
| A | 9.8 / 19.2 = 51.0% | $510.4m | $505.2m | $5.3m |
| B | 4.0 / 19.2 = 20.8% | $208.3m | $206.2m | $2.1m |
| C | 5.4 / 19.2 = 28.1% | $281.3m | $278.4m | $2.9m |

The buys add up to $10.3m, the cash received. **So an ordinary dividend causes a small trade but no divisor change.** It is the first case where the two answers differ.

## Corporate Action 4: Special Dividend

B pays a one-time **special dividend** of $10 a share, much larger than its usual payout. Assume B's price drops from $100 to $90 on the ex-date.

**Divisor?** S&P's rule is different here. For a special dividend, the stock price is adjusted by the dividend amount and **the divisor changes**:

> B's value = 40m × $90 = $3.6bn
> new total = $10.0bn + $3.6bn + $5.4bn = $19.0bn
> new divisor = $19.0bn ÷ 1,000 = **$19.0m**

The **price index stays at 1,000**. Compare this with the ordinary dividend, where the price index fell. The treatment is a convention: regular dividends are treated as income, captured only in the total return index, while one-off special dividends are taken out of the price index through the divisor.

**Fund trade?** The fund receives $10 × 2.062m shares = **$20.6m in cash** and reinvests it across the index at the new weights:

| Stock | New weight | Target | Held | Buy |
|---|---:|---:|---:|---:|
| A | 10.0 / 19.0 = 52.6% | $526.3m | $515.5m | $10.9m |
| B | 3.6 / 19.0 = 18.9% | $189.5m | $185.6m | $3.9m |
| C | 5.4 / 19.0 = 28.4% | $284.2m | $278.4m | $5.9m |

(B held = 2.062m × $90 = $185.6m.) The buys add up to $20.6m. **So a special dividend changes the divisor and causes a reinvestment trade.**

## Corporate Action 5: Spin-off

A spins off a division as a new company, A-Sub. A shareholders receive 1 A-Sub share for every 4 A shares, so 200m ÷ 4 = 50m A-Sub shares are created. Assume that after the spin-off, A trades at $45 and A-Sub at $20.

**Step 1. Value is split, not created.**

> A: 200m × $45 = $9.0bn
> A-Sub: 50m × $20 = $1.0bn
> together = **$10.0bn**, the same as A before

(Assuming the market values the two pieces at exactly what A was worth. In practice the sum can differ a little.)

**Step 2. Day one: the spin-off joins the index.** S&P adds A-Sub on the ex-date *at a price of zero*, with the same attributes as its parent and with index shares set by the spin-off ratio. At the moment it is added, its value in the index is zero, so the total doesn't change and **there is no divisor change**. When trading opens, A's price falls and A-Sub's price appears, and the two offset.

**Fund trade on day one?** None. The fund automatically receives 10.31m ÷ 4 = **2.58m A-Sub shares**, worth 2.58m × $20 = $51.5m. (Check with the slice: 5.155% of A-Sub's 50m shares = 2.58m.)

**Step 3. Later: the spin-off is usually removed.** S&P keeps the spin-off in the index for at least one trading day. If it doesn't meet the index's rules, as is likely for a $1.0bn company in an index whose entry threshold is $22.7bn, it is then deleted. Its weight is reinvested across the other members in proportion.

> new total = $19.4bn − $1.0bn = $18.4bn
> new divisor = $18.4bn ÷ 1,000 = **$18.4m** (the divisor changes now)

**Fund trade at deletion?** Yes. The fund must **sell all 2.58m A-Sub shares ($51.5m)** and reinvest the cash across A, B, and C.

The desk angle: *every* fund tracking the index sells A-Sub at the same close. That is forced, predictable selling in a newly listed and often thinly traded stock. A spin-off is the clearest example of "no divisor change today, forced flow tomorrow."

## Corporate Action 6: Mergers and Acquisitions

Takeovers are handled case by case, so this section explains the mechanism in words rather than numbers.

**Cash takeover of a member.** An outside buyer pays cash for all of C. S&P removes C around the date it stops trading. The total falls, so **the divisor changes**. Index funds end up with cash for their C shares and, because a seat is now empty, must **buy whichever company replaces C**. The addition is a separate forced purchase.

**Stock-for-stock merger between two members.** A buys C and pays in new A shares. S&P's Policies & Practices document says the acquirer's share increase is implemented at the same time as the target is dropped. The fund's C shares are swapped for A shares by the deal itself. Since the total value roughly carries over from C to the larger A, **the divisor change is small, and index funds trade little or nothing**. The deal does their rebalancing for them.

**Stock deal where the acquirer is not in the index.** If an outside company pays in its own shares, index funds receive shares of a company their index doesn't hold, so they **must sell those shares** and buy C's replacement. That flow can be large.

## Summary: The Two Tests Side by Side

Each row was worked through above (or in Lesson 9 for the first rows).

| Event | Divisor changes? | Index funds trade? |
|---|---|---|
| Price move | No | No |
| Stock split | No | No |
| Add or delete a stock | Yes | Yes |
| Share issuance / buyback | Yes | Yes (buy / sell that stock) |
| Float factor change | Yes | Yes |
| Ordinary dividend | No (price index falls) | Small: reinvest cash |
| Special dividend | Yes | Yes: reinvest cash |
| Spin-off, day one | No | No (shares arrive) |
| Spin-off removed later | Yes | Yes: sell the spin-off |
| Cash takeover | Yes | Yes: buy the replacement |
| Stock merger, both members | Small | Little or none |

The divisor answers *"did the index's total value change for a reason other than price?"* The trade test answers *"do the fund's holdings still match the target without doing anything?"* Read down the table and you'll find every combination: neither (split), both (issuance), divisor only (stock merger, roughly), and trade only (ordinary dividend reinvestment).

## Common Misconceptions

**"A divisor change means index funds are trading."** The divisor is an internal scaling number. A stock merger between two members changes it slightly with almost no trading, and an ordinary dividend causes reinvestment trades with no divisor change at all. To find flow, ask whether holdings still match the target, not whether the divisor moved.

**"Stock splits matter for index funds."** A split changes the price per share and the number of shares by the same factor. Value, weights, and holdings are all unchanged. (Splits do matter for *price-weighted* indexes such as the Dow Jones Industrial Average, which is a different design.)

**"The price index falling on an ex-dividend date is a loss."** Investors received the cash. The total return index, which is what funds are measured against, doesn't move.

**"Dividends are reinvested into the stock that paid them."** S&P's total return calculation reinvests them across the whole index, in proportion to the weights.

**"A spin-off is just bookkeeping."** On day one it is. But when the spin-off is dropped from the index, every tracker sells it at once.

**"The index level is comparable to a stock price."** The level depends on an arbitrary starting divisor. Only its *percentage changes* mean anything. A level of 6,000 isn't "expensive" compared with a level of 1,000.

## Recap

An index level is the total tradable value of its members divided by a divisor. The divisor is a scaling number that the provider adjusts whenever the total changes for any reason other than price. That keeps the level continuous, so it measures only price moves. Adding D to the toy index would have caused a fake 10.3% jump. Raising the divisor from $19.4m to $21.4m kept the level at 1,000, and the next day's 1% rise in prices showed up as exactly 1%. Whether index funds must trade is a separate question: they trade when their target holdings change in a way their existing holdings don't follow. Splits change neither the divisor nor holdings. Share issuance, buybacks, float changes, additions, and deletions change both. Ordinary dividends leave the divisor alone but require reinvesting cash. Special dividends change the divisor and also require reinvesting. Spin-offs arrive with no divisor change and often leave later as a forced sale. On a desk, the trade test is what matters. The divisor tells you the index kept its books straight. The trade test tells you who has to buy or sell.

## New Terms

**index level**: The published number for an index: total tradable value of the members divided by the divisor.

**divisor**: A scaling number, adjusted by the index provider, that keeps the index level unchanged when the total value changes for non-price reasons.

**base value / base date**: The arbitrary starting level an index is set to (such as 1,000) and the date it starts. Only percentage changes from there have meaning.

**continuity**: The property that the index level only moves because of price changes, not because of membership or corporate actions.

**corporate action**: An event initiated by a company that changes its shares, price, or structure, such as a split, dividend, share issuance, spin-off, or merger.

**stock split**: Dividing each share into several, with the price reduced by the same factor. Value is unchanged.

**ex-dividend date (ex-date)**: The first trading day on which a stock trades without the right to the next dividend. The price usually drops by about the dividend amount.

**ordinary dividend**: A regular cash dividend. In S&P indexes it causes no divisor change and is captured only in the total return index.

**special dividend**: A one-time, unusually large cash dividend. In S&P indexes the price is adjusted and the divisor changes.

**index dividend points**: The day's dividends paid by index members, divided by the divisor. This is how a total return index adds dividends back.

**spin-off**: A company separating a division into a new listed company, whose shares go to existing shareholders.

**accelerated implementation**: S&P's faster track for large share changes (at least $150m and at least 5% of shares, for offerings), applied with short notice instead of waiting for the quarterly update.

## Questions to Test Yourself

1. The toy index is at 1,000 with a $19.4m divisor. Stock B is deleted ($4.0bn of tradable value) with no price change. What is the new divisor?

The new total is $19.4bn − $4.0bn = $15.4bn, so the new divisor is $15.4bn ÷ 1,000 = $15.4m. The level stays at 1,000.

2. Why doesn't a 3-for-1 stock split cause any index fund trading?

The price falls to a third and the share count triples, so the stock's value and weight are unchanged. The fund's shares triple automatically, so its holdings still match the target.

3. An ordinary dividend doesn't change the divisor. Why do index funds still trade?

They receive cash, which the index doesn't hold. To keep tracking the total return index, they reinvest that cash across all members at the index weights.

4. A member issues new shares worth 3% of its share count, raising $500m. When do S&P 500 funds buy?

The offering meets the $150m test but not the 5% test, so it doesn't get accelerated treatment. The share change waits for the next quarterly update, after the close on the third Friday of the quarter's last month, and funds buy then.

5. Why is a spin-off often followed by selling pressure in the new company?

It enters the index at a price of zero with no divisor change, but if it is too small for the index, it is deleted soon afterward. Every tracking fund then sells it at the same close.

## Sources

S&P Dow Jones Indices. "Index Mathematics Methodology." September 2026. The Index Divisor; Capitalization Weighted Indices; Divisor Adjustments; Total Return Calculations. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-index-math.pdf)

S&P Dow Jones Indices. "Equity Indices Policies & Practices Methodology." August 2026. Mergers & Acquisitions; Material Share/IWF Changes; Non-Material Share/IWF Changes; Summary of Corporate Action Treatment for Market Capitalization Indices. [https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf](https://www.spglobal.com/spdji/en/documents/methodologies/methodology-sp-equity-indices-policies-practices.pdf)
