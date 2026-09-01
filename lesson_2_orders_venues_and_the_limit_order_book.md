# Lesson 2: Orders, Venues, and the Limit Order Book

## Learning Goal

Lesson 1 asked who is trading and why. This lesson asks how that intention becomes an executable trade.

The key idea is that "the price" is not one number when size matters. There is a last trade, a best bid, a best ask, visible depth, liquidity you cannot see, and the average price you actually get for the shares you need. On a flows desk, those distinctions decide whether a required buy looks cheap, expensive, noisy, or crowded.

## The Problem the Order Book Solves

Buyers and sellers do not all want the same thing at the same moment. Some need to trade now. Some will trade only at a price they like. The market needs a way to store those intentions and match them when they cross.

A limit order book is that matching machine for a lit venue. It is not a valuation model. It does not say what a company is worth. It shows currently available trading interest under the venue's rules.

```text
willing buyers post bids
willing sellers post offers
incoming orders match against resting interest
trades print
unmatched interest stays in the book
```

## Market Orders and Limit Orders

A market order says: trade now at the best available prices. A limit order says: trade only at this price or better.

Market orders buy certainty of execution and give up price control. Limit orders keep price control and risk not getting filled. A fund that must finish a rebalance by the close may care more about completion. A patient discretionary buyer may care more about price.

If you send a market buy, you demand liquidity. You buy from the lowest available offers first. If your size is larger than the shares at the best ask, the order continues into worse prices. If you post a buy limit, you supply liquidity at your chosen price and wait for a seller to hit you.

```text
market order
  -> demand liquidity now
  -> uncertain average price if size is large

limit order
  -> choose a price or better
  -> uncertain fill
```

## Bid, Ask, and Spread

The bid is the best displayed price where someone is willing to buy. The ask, also called the offer, is the best displayed price where someone is willing to sell. The bid-ask spread is the gap between them.

If the best bid is $99.98 and the best ask is $100.02, the spread is $0.04. An urgent seller usually hits the bid. An urgent buyer usually lifts the ask. The spread is compensation for immediacy: the liquidity provider stands ready to trade and takes inventory risk until that position is unwound or hedged.

## A Simple Order Book Walk

Suppose XYZ has this simplified book:

```text
SELLERS / OFFERS

price       shares
$100.05     1,500
$100.04     1,000
$100.03       800
$100.02       500   <- best ask

-------------------------

$99.98        700   <- best bid
$99.97      1,200
$99.96      2,000
$99.95      3,000

BUYERS / BIDS
```

A market buy of 300 shares fills entirely at $100.02, because 500 shares are offered there.

A market buy of 1,000 shares is different:

```text
500 shares at $100.02
500 shares at $100.03
average price = $100.025
```

The best ask was $100.02, but the executable average for 1,000 shares was worse because the order walked the book. That is the start of market impact: your own size consumes nearby liquidity and pushes fills into less attractive prices. Lesson 3 develops impact more fully. The point here is simpler: quoted top-of-book price is not the same as executable price for size.

## Last Price Is Not Executable Price

The last traded price is where a previous trade happened. It does not tell you how much you can trade there now.

If XYZ last traded at $100.00, that does not mean you can buy 1 million shares at $100.00. The current ask might show only 500 shares at $100.02. The rest may require walking the book, finding hidden or dark liquidity, calling a dealer, or working the order over time.

```text
last price        -> historical print
best bid / ask    -> next small trade may happen here
depth             -> how much is shown nearby
execution price   -> what your size and urgency actually get
```

For tiny trades these can be close. For index and basket flow they often are not.

## Depth, Displayed Liquidity, and Hidden Liquidity

Depth is how many shares sit at each price level. More depth near the touch usually means a given order can finish with less price movement. Less depth means the same order walks farther.

Displayed liquidity is what the public book shows. It is useful and incomplete. Some orders are hidden or only partially displayed on lit venues. Some interest sits in dark pools. Some liquidity is latent: it appears only after price moves enough to attract new buyers or sellers, or after a broker finds a willing counterparty.

```text
displayed  -> visible now in the public book
hidden     -> resting interest not fully shown
latent     -> may appear if price, venue, or search changes
```

A flows desk should treat the book as a starting map, not the whole territory.

## Queue Priority

At one price, many orders may be waiting. Most lit U.S. equity markets use price-time priority: better prices go first, and at the same price earlier orders usually go first.

```text
Trader A: buy 1,000 at $100.00, first in time
Trader B: buy 1,000 at $100.00, second
Trader C: buy 1,000 at $100.00, third
```

If a seller sells 1,500 shares at $100.00, A gets 1,000, B gets 500, and C gets nothing. Being at the right price is not enough. You also need enough opposite-side flow to reach your place in the queue. That is one reason patient limit orders can miss fills even when the print eventually trades through your price on another venue or later in the day.

## Lit Exchanges, Dark Pools, ATSs, and Off-Exchange Trading

Not all trading happens in one place.

A lit exchange displays bids and offers publicly in a central limit order book. That pre-trade transparency helps price discovery: other participants can see where displayed interest sits.

A dark pool is an alternative trading system (ATS) that matches orders without showing a public book the way a lit exchange does. Under U.S. Regulation ATS, many dark venues register as broker-dealers and do not disseminate quotes to the public. Trades still report to the consolidated tape after execution, often through a FINRA Trade Reporting Facility, but without the same pre-trade display. Large traders use dark venues partly to reduce information leakage: posting a huge bid on a lit book can advertise demand and move price before the trade is done.

Off-exchange trading is broader than dark pools. It includes dark ATSs, broker internalization, wholesaler execution, and other non-exchange matching. Optiver-style wholesale or direct-counterparty trades sit in this broader family: size can be negotiated away from the public book, then reported after the fact. The tradeoff is the same shape every time. You may reduce leakage and find block size, but you give up some certainty about whether liquidity is there, and you may face adverse selection if the other side is better informed.

```text
lit exchange
  -> public book, clearer displayed depth, more leakage risk for large size

dark pool / non-display ATS
  -> less pre-trade visibility, possible block matching, uncertain fill

other off-exchange
  -> internalization, RFQ, bilateral liquidity; post-trade print, not a public queue
```

Venue choice is part of the trade, not an afterthought. It changes what information you reveal, how likely you are to finish, what price you get, and how much the rest of the market can see coming.

## Why This Matters for Index and Rebalance Flow

Index and rebalance trades often combine three hard constraints: large size, known direction, and a deadline tied to a closing benchmark.

If a stock is added to an index, passive funds may need to buy by the effective close. Displayed book depth may cover only a fraction of that demand. The rest has to come from hidden interest, dark or bilateral liquidity, dealers warehousing risk, or the closing auction. If the fund shows too much too early on lit venues, other traders can lean ahead of the flow. If it hides too much and waits too long, completion risk rises into the close.

```text
required index trade
  -> execution choice: lit / dark / bilateral / auction
  -> orders interact with depth and queues
  -> liquidity providers adjust quotes and inventory
  -> average price and residual risk emerge
```

Knowing that mechanical demand exists is only step one. Microstructure is how that demand meets supply.

## Common Misconceptions

The stock price is not one number for a large order. Last price, top of book, and your executable average can diverge quickly once size exceeds nearby depth.

A market order does not always fill entirely at the best bid or ask. It only does that if enough size is there. Larger orders walk the book.

Displayed liquidity is not total liquidity. Hidden, dark, and latent interest can matter, but they are not guaranteed and are not free of adverse selection.

Dark pools are not automatically better. They can reduce leakage and help source size, but they do not guarantee a fill or a better price.

## Recap

Orders turn a motive into a claim on liquidity. Market orders demand immediacy; limit orders post price conditions and wait. The lit book stores bids and offers, the spread prices immediacy, and depth tells you how far a given size must walk. Queue priority decides who gets served first at a price. Venues matter because lit, dark, and other off-exchange mechanisms reveal different amounts of information and offer different fill certainty. For flows trading, especially index and rebalance flow, the practical question is never only "what is the price?" It is "what can I actually execute, where, by when, and what will that reveal?"

## New Terms

**market order**: An order to trade immediately at the best available prices.

**limit order**: An order to trade only at a stated price or better.

**bid**: The best displayed price at which someone is willing to buy.

**ask / offer**: The best displayed price at which someone is willing to sell.

**bid-ask spread**: The difference between the best ask and the best bid. It is part of the cost of trading immediately.

**limit order book**: The venue's schedule of resting buy and sell limit orders, ranked by price and usually by time within each price.

**depth**: How many shares are available at each price level in the book.

**displayed liquidity**: Trading interest visible in the public order book.

**hidden liquidity**: Resting interest that is available to trade but not fully shown publicly.

**latent liquidity**: Potential trading interest that may appear if price, search, or venue conditions change.

**queue priority / price-time priority**: The rule that better-priced orders trade first, and earlier orders at the same price usually trade before later ones.

**lit exchange**: A venue that publicly displays bids and offers in a central limit order book.

**dark pool**: An ATS that matches orders without a public pre-trade book like a lit exchange. Trades still report after execution.

**alternative trading system (ATS)**: A non-exchange trading venue regulated under rules such as Regulation ATS. Dark pools are usually non-display ATSs.

**off-exchange trading**: Trading away from registered exchanges, including dark ATSs, internalization, and bilateral or wholesale liquidity.

**walking the book**: Consuming multiple price levels with one aggressive order because size exceeds depth at the best price.

## Questions to Test Yourself

1. What is the difference between a market order and a limit order?

A market order demands immediate execution at whatever prices are available. A limit order sets a price condition and may not fill.

2. Why does the bid-ask spread exist?

Urgent traders pay for immediacy. Liquidity providers earn the spread as compensation for standing ready to trade and taking inventory risk.

3. Why can a 1,000-share market buy receive a worse average price than the best ask?

If fewer than 1,000 shares are offered at the best ask, the order buys the rest at worse prices. The average fill is then above the top-of-book ask.

4. What is the difference between displayed, hidden, and latent liquidity?

Displayed liquidity is shown in the public book. Hidden liquidity is resting but not fully shown. Latent liquidity may appear only after price, venue, or search conditions change.

5. Why might a trader use a dark pool instead of a lit exchange?

To reduce pre-trade information leakage on large size and to search for a match without advertising full demand on a public book. The cost is less certainty about fill and displayed depth.

6. Why does queue priority matter?

Being at the right price does not guarantee a fill if other orders arrived earlier at that price. You need enough opposite-side flow to reach your place in line.

7. Why do index and rebalance trades care about venue and the close?

They often combine large size, known direction, and a closing-price benchmark. Venue choice affects leakage and fill quality, and much benchmark-sensitive flow concentrates near the closing auction.
