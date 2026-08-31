# Lesson 2: Orders, Venues, and the Limit Order Book

## Learning Goal

This lesson explains how a desire to buy or sell becomes an actual trade.

Lesson 1 focused on the people and institutions behind market flow. This lesson moves one level closer to the machinery of the market: orders, prices, venues, and the limit order book. The key idea is that "the price" is not a single thing when you are trading size. There is a last traded price, a best bid, a best ask, visible depth, hidden liquidity, and the price you can actually execute for the amount you need.

That distinction matters constantly on a flows desk. A client may want to buy 2 million shares, but the market may only show a few thousand shares available near the current price. The desk has to think about size, urgency, venue choice, information leakage, and market impact.

## The Basic Problem

Markets need a way to organize buyers and sellers.

Some buyers want to trade immediately. Some buyers only want to buy if the price is low enough. Some sellers want to sell immediately. Some sellers only want to sell if the price is high enough.

The limit order book is one mechanism for organizing those intentions.

```text
buyers willing to pay certain prices
   |
   v
bids in the order book

sellers willing to accept certain prices
   |
   v
offers in the order book

incoming orders
   |
   v
match against available bids or offers
```

The order book is not a valuation model. It does not tell you what a company is worth. It shows currently available trading interest under the rules of a venue.

## Market Orders and Limit Orders

A market order says: trade now at the best available prices.

A limit order says: trade only at this price or better.

That is the basic tradeoff. Market orders prioritize execution certainty. Limit orders prioritize price control.

If you send a market buy order, you are demanding liquidity from sellers. You will trade against the lowest available offers first. If your order is larger than the shares available at the best offer, it will continue into higher prices.

If you place a buy limit order, you are saying the maximum price you are willing to pay. You may get a better price, but you may not get filled.

```text
market order
  -> more certainty of execution
  -> less control over final price

limit order
  -> more control over price
  -> less certainty of execution
```

This tradeoff is everywhere in execution. A fund that must complete a rebalance by the close may care more about completion. A patient investor may care more about price.

## Bid, Ask, and Spread

The bid is the best displayed price where someone is willing to buy.

The ask, also called the offer, is the best displayed price where someone is willing to sell.

The bid-ask spread is the difference between them.

If the best bid is $99.98 and the best ask is $100.02, the spread is $0.04. A trader who wants to sell immediately usually hits the bid. A trader who wants to buy immediately usually lifts the offer.

The spread is partly the cost of immediacy. If you demand liquidity right now, you usually pay for that convenience. The liquidity provider earns the spread as compensation for standing ready to trade and for taking inventory risk.

## A Simple Order Book

Suppose stock XYZ has this simplified order book:

```text
SELLERS / OFFERS

price       shares offered
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

The best bid is $99.98. The best ask is $100.02. The spread is $0.04.

If you send a market order to buy 300 shares, you can buy all 300 at $100.02 because there are 500 shares offered there.

If you send a market order to buy 1,000 shares, the trade is different. You buy 500 shares at $100.02, then you still need 500 more. The next offer is $100.03, so you buy 500 shares there.

Your fill is:

```text
500 shares at $100.02
500 shares at $100.03
```

Your average price is:

```text
((500 * 100.02) + (500 * 100.03)) / 1000 = $100.025
```

The best ask was $100.02, but your average execution price was $100.025 because your order was larger than the shares available at the best ask.

This is the beginning of market impact. Your own order consumes liquidity and pushes your execution into worse prices.

## Last Price Is Not Executable Price

The last traded price tells you where the most recent trade occurred. It does not tell you how much you can trade there now.

If the last trade in XYZ was at $100.00, that does not mean you can buy 1 million shares at $100.00. The current ask might be $100.02, with only 500 shares displayed. The next 999,500 shares may require higher prices, hidden liquidity, a broker search, or patient execution over time.

This distinction is basic but important. Charts show historical prints. Traders need executable liquidity.

```text
last price
  -> where a previous trade happened

best bid and ask
  -> where the next small trade may happen

depth
  -> how much is available at nearby prices

execution price
  -> what you actually get for your size and urgency
```

For small trades, these may be close together. For large flows, they can be very different.

## Depth and Displayed Liquidity

Depth means the number of shares available at different price levels.

The best ask might show 500 shares. The next ask might show 800 shares. A few cents higher, there may be several thousand shares. The deeper you go into the book, the more size may be available, but usually at worse prices.

Displayed liquidity is the liquidity visible in the public order book. It is useful because it shows some immediate supply and demand, but it is incomplete.

Some liquidity is hidden. Some sits in dark pools. Some belongs to participants who are willing to trade but do not want to display their full size. Some appears only after price moves enough to attract new sellers or buyers.

A useful mental model is:

```text
displayed liquidity
  -> visible now

hidden liquidity
  -> available but not fully shown

latent liquidity
  -> may appear if the price becomes attractive
```

For a flows desk, this means the order book is a starting point, not the whole map.

## Queue Priority

At a given price, there may be many orders waiting.

Suppose three traders place buy limit orders at $100.00:

```text
Trader A: buy 1,000 shares at $100.00, submitted first
Trader B: buy 1,000 shares at $100.00, submitted second
Trader C: buy 1,000 shares at $100.00, submitted third
```

If a seller sells 1,500 shares at $100.00, Trader A gets filled first. Trader B gets the remaining 500 shares. Trader C gets nothing.

That is queue priority. Many markets use price-time priority: better prices go first, and within the same price, earlier orders usually go first.

Queue priority matters because placing a limit order at the right price does not guarantee a fill. You also need enough incoming opposite-side flow to reach your place in the queue.

## Lit Venues, Dark Pools, and Off-Exchange Trading

Not all trading happens in the same place.

A lit exchange displays bids and offers publicly. Lit markets help price discovery because participants can see displayed supply and demand.

A dark pool matches buyers and sellers without displaying the same kind of public order book. Dark pools can help large traders reduce information leakage. If a large buyer reveals its full demand in the lit market, other traders may react and push the price higher.

Off-exchange trading includes dark pools, broker internalization, single-dealer platforms, and other non-exchange venues. These venues can provide useful liquidity, but they come with tradeoffs: uncertain fill probability, less visible liquidity, different matching rules, and possible adverse selection.

Venue choice is not a minor operational detail. It affects how much information the order reveals, how quickly it fills, what price it receives, and how much market impact it creates.

## Why Venue Choice Matters for Flows

Imagine a fund needs to buy a large basket before a rebalance close.

If the fund displays too much interest too early, other traders may infer the flow and move prices. If it waits too long, it may face a crowded closing auction. If it uses dark pools, it may reduce information leakage but may not find enough liquidity. If it uses market orders aggressively, it may complete the trade but pay more impact.

The execution problem is a balance:

```text
complete the trade
  -> avoid too much price impact
  -> avoid revealing too much information
  -> manage benchmark risk
  -> find enough liquidity
```

That balance changes depending on whether the trade is discretionary, benchmark-sensitive, or forced.

## Connection to Index and Rebalance Trading

Index rebalances often create trades with size and timing constraints.

If a stock is added to an index, passive funds may need to buy it by the effective date. If those funds care about tracking the closing benchmark, much of the flow may concentrate near the close or in the closing auction.

The order book and venue structure determine how that demand meets supply. Displayed liquidity may absorb only a small part of the flow. Hidden liquidity, dealers, arbitrageurs, market makers, and auctions may absorb the rest.

The practical chain looks like this:

```text
index rule creates required trade
   |
   v
fund or desk chooses execution strategy
   |
   v
orders interact with venues and liquidity
   |
   v
market makers and other traders adjust
   |
   v
execution price and market impact emerge
```

This is why market microstructure matters for index mechanics. Knowing that a fund needs to buy is only the first step. The next question is how that buying actually gets done.

## Common Misconceptions

It is easy to think the stock price is one number. For a tiny trade, that shortcut may be fine. For a large trade, price depends on size, urgency, venue, and available liquidity. The last price on a chart is not the same as the price for a large executable order.

Another common mistake is assuming a market order fills entirely at the best bid or ask. It only does that if enough shares are available at that price. A larger order walks the book and receives multiple prices.

Displayed liquidity is also not the same as total liquidity. The public book shows what participants are willing to reveal. Hidden, dark, and latent liquidity may exist, but accessing it depends on venue choice and execution strategy.

Finally, dark pools are not automatically better. They may reduce information leakage, but they do not guarantee fills or superior prices. A trader still has to think about adverse selection, urgency, and opportunity cost.

## Questions to Test Yourself

1. What is the difference between a market order and a limit order?
2. Why does the bid-ask spread exist?
3. Why can a 1,000-share market buy order receive a worse average price than the best ask?
4. What is the difference between displayed, hidden, and latent liquidity?
5. Why might a trader use a dark pool instead of a lit exchange?
6. Why does queue priority matter?
7. Why do index and rebalance trades often care about the closing auction?

## Recap

The limit order book organizes visible buying and selling interest. Bids show where buyers are willing to buy, offers show where sellers are willing to sell, and the spread is the gap between the best two prices. A market order demands liquidity immediately, while a limit order supplies liquidity at a chosen price but may not get filled.

For small trades, the quoted price may be close to the execution price. For large flows, the difference can be meaningful. Size can consume multiple price levels, displayed liquidity may understate or overstate true trading interest, and venue choice can change both information leakage and fill quality.

This lesson connects directly to flows trading because every index rebalance, ETF basket trade, hedge, or client portfolio trade eventually becomes orders interacting with liquidity. The desk's job is not just to know that flow exists. It is to understand how that flow will reach the market, where liquidity may come from, and how execution choices can change the final price.
