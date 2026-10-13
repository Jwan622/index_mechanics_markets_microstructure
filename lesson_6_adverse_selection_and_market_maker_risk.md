# Lesson 6: Adverse Selection and Market Maker Risk

## Learning Goal

Lesson 5 treated the dealer's problem as inventory: the price might wander before the position is gone. This lesson adds a second, nastier risk. The price might not wander at random. It might move against the dealer *because* the person on the other side knew it would.

That is adverse selection. It explains why spreads exist even for a market maker with no inventory problem, why spreads widen when uncertainty rises, why liquidity providers care so much about *who* is trading, and why liquidity can vanish exactly when someone needs it. It also explains a fact that matters a lot on a flows desk: flow that is known to be uninformed, like an index rebalance, can be cheaper to trade than flow of the same size that might be informed.

## The Problem: Who Fills Your Quote?

A market maker shows $99.95 bid / $100.05 ask on XYZ. Lesson 5's picture was that buyers and sellers arrive roughly at random, the market maker earns the spread, and inventory risk is the main cost.

Now ask who actually chooses to trade against that quote.

Someone who thinks XYZ is worth $100 has no strong reason to lift a $100.05 offer. Someone who has just read a strong earnings release and thinks XYZ is worth $103 will lift it as fast as possible and for as much size as is shown. The quote is the same for everyone, but the people who accept it are not a random sample. They are *selected*, and the selection works against the person quoting. That is where the name comes from: adverse selection means the trades you get are disproportionately the ones you would have refused if you knew what the other side knew.

The same idea appears outside markets. An insurer offering one price to everyone attracts more of the people who expect to make claims. A used-car buyer offering one price attracts more of the bad cars. A market maker offering one price attracts more of the traders who know the price is wrong.

## A Small Worked Example: Pricing a Quote with Bayes' Rule

This is the Glosten and Milgrom (1985) model, which Lesson 4 mentioned in one paragraph. Here we work it with numbers, because the mechanism is all in the arithmetic.

**The setup.** XYZ will soon be revealed to be worth either $110 (good news) or $90 (bad news). Right now each is equally likely, so the market maker's best guess is $100. Traders arrive one at a time and each trades one unit.

- 30% of traders are **informed**: they know the true value. They buy if it is $110 and sell if it is $90.
- 70% are **uninformed**: they trade for their own reasons (cash needs, rebalances, hedges). They buy or sell with equal probability, regardless of the true value.

The market maker cannot tell the two types apart. Competition with other market makers forces quotes to the level where expected profit is zero.

**Step 1: How likely is a buy in each world?**

If the value is $110, every informed trader buys and half the uninformed traders buy:

```text
P(buy | value = 110) = 0.30 + 0.70 * 0.5 = 0.65
```

If the value is $90, no informed trader buys. Only the uninformed half does:

```text
P(buy | value = 90) = 0.70 * 0.5 = 0.35
```

Overall, P(buy) = 0.5 × 0.65 + 0.5 × 0.35 = 0.50.

**Step 2: What does a buy tell you?** Bayes' rule turns "how likely is a buy in each world" into "how likely is each world, given that I just saw a buy":

```text
P(value = 110 | buy) = P(buy | 110) * P(110) / P(buy)
                     = 0.65 * 0.5 / 0.50
                     = 0.65
```

Before the trade, good news was 50/50. After seeing someone buy, it is 65/35. The buy order itself is evidence.

**Step 3: Set the ask.** The market maker should sell at what the stock is worth *conditional on someone wanting to buy*, not at the unconditional $100:

```text
ask = 0.65 * 110 + 0.35 * 90 = 71.5 + 31.5 = $103
```

By symmetry the bid is $97. The spread is $6, even though this market maker has no inventory cost, no fees, and no risk aversion. The whole spread pays for information.

**Step 4: Check that the market maker breaks even.** Out of every 100 buys at $103, 30 come from informed traders who only buy when the value is $110, so the market maker loses $7 on each. The other 70 come from uninformed traders, and on average the stock is worth $100 to them, so the market maker earns $3 on each:

```text
expected profit per buy = 0.30 * (103 - 110) + 0.70 * (103 - 100)
                        = -2.10 + 2.10
                        = 0
```

This is the core accounting identity of adverse selection: **uninformed traders pay the spread, and that payment funds the losses to informed traders.** The market maker is only the pipe.

## The General Result, Proved

Now replace the numbers with symbols. Let the value be H or L with equal probability, and let μ be the fraction of informed traders.

```text
P(buy | H) = μ + (1 - μ)/2 = (1 + μ)/2
P(buy | L) = (1 - μ)/2
P(buy)     = 1/2
P(H | buy) = [(1 + μ)/2 * 1/2] / (1/2) = (1 + μ)/2
```

So the ask is:

```text
ask = L + P(H | buy) * (H - L) = L + (1 + μ)/2 * (H - L)
```

The same steps on the sell side give P(H | sell) = (1 − μ)/2, so:

```text
bid = L + (1 - μ)/2 * (H - L)

spread = ask - bid = μ * (H - L)
```

With μ = 0.30 and H − L = $20, that is $6, matching the worked example. The formula says two things a trader should remember:

1. The spread grows with **how much informed trading there is** (μ). More informed traders, wider spread.
2. The spread grows with **how much there is to know** (H − L). Before earnings, a drug trial, or an index announcement, the possible gap in value is larger, so the spread is wider even if the share of informed traders has not changed.

The symmetric 50/50 prior was a simplifying assumption that keeps the algebra short. With an uneven prior the formulas are messier, but the two conclusions hold.

A tiny Python version, for checking other numbers:

```python
def glosten_milgrom_quotes(high_value, low_value, prob_high, informed_fraction):
    """Bid and ask that leave a competitive market maker with zero expected profit."""
    uninformed_fraction = 1 - informed_fraction

    prob_buy_if_high = informed_fraction + uninformed_fraction / 2
    prob_buy_if_low = uninformed_fraction / 2
    prob_buy = prob_high * prob_buy_if_high + (1 - prob_high) * prob_buy_if_low
    prob_high_given_buy = prob_high * prob_buy_if_high / prob_buy
    ask = prob_high_given_buy * high_value + (1 - prob_high_given_buy) * low_value

    prob_sell_if_high = uninformed_fraction / 2
    prob_sell_if_low = informed_fraction + uninformed_fraction / 2
    prob_sell = prob_high * prob_sell_if_high + (1 - prob_high) * prob_sell_if_low
    prob_high_given_sell = prob_high * prob_sell_if_high / prob_sell
    bid = prob_high_given_sell * high_value + (1 - prob_high_given_sell) * low_value

    return bid, ask


glosten_milgrom_quotes(110, 90, 0.5, 0.0)   # (100.0, 100.0)  no informed traders, no spread
glosten_milgrom_quotes(110, 90, 0.5, 0.3)   # (97.0, 103.0)
glosten_milgrom_quotes(110, 90, 0.5, 0.6)   # (94.0, 106.0)
```

## How Prices Learn From Trades

The model also explains price discovery in motion. After the first buy, the market maker's belief that the value is $110 is no longer 0.50. It is 0.65. That posterior becomes the prior for the next trade.

If the next trader also buys:

```text
P(H | second buy) = 0.65 * 0.65 / (0.65 * 0.65 + 0.35 * 0.35)
                  = 0.4225 / 0.5450
                  ≈ 0.775

next ask ≈ 90 + 0.775 * 20 ≈ $105.50
```

The quotes ratchet up with each buy. If the true value really is $110, informed buying keeps tilting the order flow, and the price converges toward $110 without anyone ever announcing the news. That is the mechanism behind Lesson 4's statement that orders forecast prices: a market maker who did *not* move the quote after a run of buys would keep selling cheap to people who know better.

```text
informed trader learns value is high
   |
   v
buys more often than sells
   |
   v
market maker sees order imbalance, updates belief
   |
   v
quotes move up
   |
   v
price drifts toward true value; informed profit shrinks
```

The uncomfortable corollary for a flows desk: the market maker cannot see *why* the run of buys is happening. A large uninformed buyer, such as an index fund buying an add, produces the same tilt in order flow. The market maker updates the same way, and the uninformed buyer pays for that update. This is one reason Lesson 3's market impact exists even for trades that carry no news.

## A Quote Is a Free Option

Copeland and Galai (1983) gave a second way to see the same cost. A posted bid of $99.95 for 1,000 shares is a promise: anyone may sell you 1,000 shares at $99.95 until you cancel. That is a put option you have given to the whole market for free. A posted offer is a free call option.

Options get exercised when they are in the money. If XYZ's value drops to $99.50 and your bid is still sitting at $99.95, someone will sell to you. If the value rises to $100.50, nobody will. Your quote gets hit precisely when it is wrong. The spread is the option premium you charge to make up for this, and a wider spread or smaller size is how you charge more.

This framing makes two risks concrete.

**News risk.** Option value rises with volatility. Before an earnings release, a central bank decision, or an index announcement, the value can jump further, so the free option you are writing is worth more. Market makers widen, shrink size, or pull quotes ahead of scheduled events.

**Stale-quote risk (latency).** Even without private information, a quote can be wrong for a few microseconds after public information changes, for example when index futures move and the stock quote has not yet updated. Fast traders race to trade against the stale quote before the market maker can cancel it. Budish, Cramton, and Shim (2015) argued that this race is built into continuous limit order books. Aquilina, Budish, and O'Neill measured it on London Stock Exchange data: races averaged about 79 microseconds, made up about a fifth of FTSE 350 trading volume, and amounted to a cost of about 0.53 basis points of traded volume. They estimated it at roughly $5 billion a year across global equities. That cost lands on whoever is quoting, and they pass it on through wider spreads. This is why market makers spend so much on speed: in the free-option picture, faster cancellation shortens the life of the option they are writing.

## Measuring Toxic Flow: Markouts

"Toxic flow" is desk slang for order flow that tends to be informed, so trading against it loses money on average. You cannot see a trader's information directly, and one fill tells you almost nothing. What you can see is what the price did *after* you traded.

A markout measures this. For each fill, compare the fill price to the mid some time later (one second, one minute, the close), signed so that positive means the trade was good for you. A market maker that sold at $100.05 and sees the mid at $100.00 a minute later has a +$0.05 markout. If the mid is $100.20, the markout is −$0.15: the buyer knew something, or at least the price moved their way.

```python
def average_markout_per_share(our_fills, mid_after_fill_by_id):
    """Positive means our fills were good on average; negative means we were picked off."""
    total_markout_dollars = 0.0
    total_shares = 0
    for fill in our_fills:
        side_sign = 1 if fill["our_side"] == "buy" else -1
        later_mid = mid_after_fill_by_id[fill["fill_id"]]
        total_markout_dollars += side_sign * (later_mid - fill["fill_price"]) * fill["shares"]
        total_shares += fill["shares"]
    return total_markout_dollars / total_shares


index_fund_fills = [
    {"fill_id": 1, "our_side": "sell", "fill_price": 100.05, "shares": 1_000},
    {"fill_id": 2, "our_side": "buy", "fill_price": 99.95, "shares": 1_000},
]
hedge_fund_fills = [
    {"fill_id": 3, "our_side": "sell", "fill_price": 100.05, "shares": 1_000},
    {"fill_id": 4, "our_side": "sell", "fill_price": 100.15, "shares": 1_000},
]
mid_one_minute_later = {1: 100.00, 2: 100.01, 3: 100.20, 4: 100.35}

average_markout_per_share(index_fund_fills, mid_one_minute_later)   # about +0.055
average_markout_per_share(hedge_fund_fills, mid_one_minute_later)   # about -0.175
```

The first counterparty is paying the spread and leaving. The second keeps buying just before the price rises. Across thousands of fills, these averages separate clients and venues by how informed their flow is. That is why liquidity providers price segmented flow differently: retail orders routed to wholesalers, a dealer's known clients, and anonymous lit-market flow get different prices because their markouts differ. Easley, Kiefer, O'Hara, and Paperman (1996) formalized a related idea, the probability of informed trading (PIN), estimated from how unbalanced buys and sells are on different days.

Two cautions. Markouts mix adverse selection with inventory: a large uninformed sell order still pushes the price down after you buy from it, so a negative markout can come from impact rather than information. And the horizon matters. A fill that looks bad after one second can look fine after an hour, and vice versa.

## How Market Makers Protect Themselves

Every defense is a way to write a cheaper free option, or to write it only to people who are less likely to exercise it smartly.

They **widen the spread**, which raises the price of the option. They **show less size**, which caps the loss on any one fill. They **lean quotes after one-sided flow**, as in the Bayes example, which is updating rather than stubbornness. They **cancel faster** and invest in latency, which shortens the time a stale quote can be hit. They **step back around scheduled events**, when H − L is largest. And they **price by counterparty** where the market structure allows it, giving better prices to flow with good markouts.

## Why Liquidity Disappears When It Is Needed

Put Lesson 5 and this lesson together. In a calm market, inventory is easy to hedge and most flow is uninformed. In a stress event, both costs rise together: volatility makes inventory more dangerous, and the chance that a one-sided flow reflects real information rises. The rational response to both is to quote wider, smaller, or not at all.

The joint SEC and CFTC report on the May 6, 2010 Flash Crash described this in practice. A large trader started an algorithm to sell 75,000 E-mini S&P 500 futures contracts, about $4.1 billion, targeting 9% of the previous minute's volume without regard to price or time. As prices fell, liquidity providers that had absorbed the early selling began reducing their exposure, and some withdrew. In some individual stocks, liquidity thinned so much that trades executed at placeholder "stub" quotes as low as a penny.

```text
one-sided flow + rising volatility
   |
   v
market makers fear inventory loss AND informed counterparties
   |
   v
spreads widen, size drops, some quotes pulled
   |
   v
the same order now moves price more
   |
   v
larger price moves look like information -> more withdrawal
```

The feedback loop is the point. Liquidity is not a stock of shares sitting somewhere. It is a set of decisions by people who are deciding, moment to moment, whether the person on the other side knows more than they do.

## Why This Matters for Index Flow

Index rebalance flow is about as close to provably uninformed as large flow gets. The index provider publishes the rules, the announcement, and the effective date. The tracker buys an add because the rulebook says so, not because it has learned something about the company.

That changes the adverse-selection math. If a liquidity provider can be confident a large order is mechanical, μ for that order is close to zero, and the only remaining cost is inventory risk from Lesson 5. Admati and Pfleiderer (1991) studied this as "sunshine trading": a liquidity trader who pre-announces an order can reduce its cost, because announcing it signals that the order is not information-driven and attracts liquidity to the other side. Closing auctions, which Lesson 7 covers, are partly an institutional version of that idea: a scheduled, public, imbalance-publishing event where mechanical flow meets liquidity providers who know what it is.

The subtle point is that being uninformed is not the same as being cheap. Predictable flow avoids the information charge but invites anticipation (Lesson 3 and later Lesson 16). The desk's job is to tell the two costs apart: is a price concession paying for possible information, or for inventory and crowding around a known event?

## Common Misconceptions

A common mistake is to think the market maker loses on every informed trade and so the market maker is the victim. In a competitive market, the market maker breaks even on average. The uninformed traders are the ones who pay, through the spread, for the losses to informed traders.

Another is to label any fill that later loses money as "toxic." One fill is noise. Toxicity is a statistical property over many fills, and a negative markout can also come from inventory and impact.

It is tempting to think wider spreads before events mean market makers are being greedy. The Glosten-Milgrom formula says the spread should scale with H − L, the size of what can be learned. Wider spreads before scheduled news are the model working as intended.

Adverse selection is not only about insiders with illegal information. Most informed trading is legal: better analysis, faster reaction to public news, or knowing your own large future order flow. The futures-to-stock stale-quote race involves no private information at all.

## Recap

Adverse selection is the risk that the traders who choose to hit your quote are disproportionately the ones who know your quote is wrong. In the Glosten-Milgrom model, a market maker with no inventory cost still has to quote a spread equal to the share of informed traders times the size of the possible value gap, and the uninformed traders pay for it. Each trade updates the market maker's belief, which is why quotes drift in the direction of order flow and why even uninformed flow moves price. A resting quote is a free option; it gets exercised when news arrives or when it goes stale, which is why market makers widen before events and invest in speed. Desks measure toxicity with markouts across many fills. In stress, inventory and information risk rise together, liquidity providers withdraw, and the withdrawal amplifies the move. Index flow is valuable to understand because it is largely uninformed, which removes most of the information charge but not the inventory and anticipation costs.

## New Terms

**adverse selection**: The tendency for the trades you receive to be the ones that are worse for you, because better-informed traders choose when to trade against your quote.

**informed trader**: A trader whose order reflects knowledge about value that the quoting side lacks.

**uninformed / liquidity trader**: A trader who trades for reasons unrelated to private information, such as cash flows, hedging, or index tracking.

**toxic flow**: Desk slang for order flow that is informed on average, so trading against it loses money after the fill.

**markout**: The signed change from the fill price to the mid at a later time, used to measure whether fills were good or bad for the liquidity provider.

**free option of a quote**: The idea that a resting bid or offer lets anyone trade at that price until it is cancelled, so it is exercised when the price is wrong.

**stale quote / latency arbitrage**: Trading against a quote that has not yet updated to public information, in the short window before its owner can cancel.

**PIN (probability of informed trading)**: A model-based estimate of the share of order flow that comes from informed traders, inferred from buy and sell imbalances.

**sunshine trading**: Pre-announcing a trade to signal that it is not information-driven, which can reduce its cost.

## Questions to Test Yourself

1. Why is selling to an informed buyer dangerous?

They only buy when the stock is worth more than your offer, so every such fill loses money on average. You recover those losses only by charging every buyer a higher ask, which is the adverse-selection part of the spread.

2. Why do spreads widen when uncertainty rises?

The adverse-selection spread is the informed share times the possible value gap. When the gap grows, such as before earnings or an index announcement, the same quote is a more valuable free option, so the market maker charges more for it.

3. How do market makers protect themselves?

They widen, show less size, lean after one-sided flow, cancel faster, step back around scheduled events, and price flow by its measured markouts. Each of these makes the option they are writing cheaper or harder to exploit.

4. Why can liquidity disappear when it is most needed?

In stress, inventory risk and the chance of trading against information rise together, so the rational response is to quote less. That makes each order move price more, which looks like information and causes further withdrawal.

## Sources

Glosten, Lawrence R., and Paul R. Milgrom. 1985. "Bid, Ask and Transaction Prices in a Specialist Market with Heterogeneously Informed Traders." *Journal of Financial Economics* 14 (1): 71–100. https://doi.org/10.1016/0304-405x(85)90044-3

Copeland, Thomas E., and Dan Galai. 1983. "Information Effects on the Bid-Ask Spread." *Journal of Finance* 38 (5): 1457–1469. https://cris.huji.ac.il/en/publications/information-effects-on-the-bidask-spread/

Budish, Eric, Peter Cramton, and John Shim. 2015. "The High-Frequency Trading Arms Race: Frequent Batch Auctions as a Market Design Response." *Quarterly Journal of Economics* 130 (4): 1547–1621. https://conference.nber.org/conf_papers/f69665.pdf

Aquilina, Matteo, Eric Budish, and Peter O'Neill. "Quantifying the High-Frequency Trading 'Arms Race'." NBER Working Paper 29011; FCA Occasional Paper No. 50. Summary: https://www.nber.org/digest/202110/race-exploit-stock-price-differences-between-exchanges

Easley, David, Nicholas M. Kiefer, Maureen O'Hara, and Joseph B. Paperman. 1996. "Liquidity, Information, and Infrequently Traded Stocks." *Journal of Finance* 51 (4): 1405–1436.

Admati, Anat R., and Paul Pfleiderer. 1991. "Sunshine Trading and Financial Market Equilibrium." *Review of Financial Studies* 4 (3): 443–481. https://ideas.repec.org/a/oup/rfinst/v4y1991i3p443-81.html

U.S. Commodity Futures Trading Commission and U.S. Securities and Exchange Commission. 2010. "Findings Regarding the Market Events of May 6, 2010." https://www.sec.gov/news/studies/2010/marketevents-report.pdf
