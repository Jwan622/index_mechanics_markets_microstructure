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

A lit exchange shows bids and offers publicly. Everyone can see the displayed book.

A dark pool is a private matching venue. Orders are not shown on a public book the way they are on an exchange. If a buyer and a seller both happen to be there, they can match, often near the middle of the bid-ask spread. If nobody is on the other side, you wait. Trades still print on the public tape after they happen.

### What "off-exchange" means

Off-exchange simply means the trade was not matched on a registered exchange's public book. Dark pools are one off-exchange path. There are others. The important split is:

- **matching venues**, where you hope another order is already there
- **principal venues**, where a firm takes the other side with its own capital

Optiver is an example of a principal liquidity provider: a market-making firm that quotes prices and takes inventory risk. Jane Street is another. A bank trading desk can play a similar role. They are not the exchange, and they are not your retail brokerage app.

A retail broker is the firm ordinary investors use to place stock orders, such as Robinhood, Fidelity, or Schwab. An institutional broker helps large funds trade. Those are different businesses from a market maker like Optiver, though they interact constantly.

### Simple scenarios

**1. Dark pool**

A pension fund wants to buy 200,000 shares quietly. It sends the order to a dark pool. If another institution is already selling there, they may match near $100.00 midpoint. If not, nothing happens. The fund did not get a promise that the trade would finish.

**2. Broker internalization**

You tell your broker, "Buy 500 shares of XYZ." Instead of sending your order to Nasdaq or NYSE, the broker fills you from its own inventory. You bought from the broker. The broker is long or short afterward and has to manage that risk.

**3. Wholesaler execution (common for retail)**

You click buy 100 shares in a retail brokerage app. The retail broker often does not take the other side itself. It routes your order to a wholesale market maker. That wholesaler buys or sells against you as principal, then hedges or manages the inventory. This is a major path for small retail orders. It is usually not how a pension fund moves a giant block.

**4. Wholesale block / RFQ**

A pension fund needs to sell 500,000 shares now. Its broker calls or messages several market makers: "Firm quote on 500,000 XYZ?" Optiver, Jane Street, or a bank desk may reply with a two-way price. The broker lifts one offer. That market maker owns the stock immediately and must hedge. The fund got size certainty. It probably paid away from mid for that certainty.

**5. Direct counterparty (DCP)**

Same idea as a wholesale block, but without the broker in the middle, and usually continuous rather than one-off. A large asset manager connects its trading system directly to Optiver. All day, Optiver streams a live bid and ask in size. When the manager wants to sell 600,000 shares, it hits Optiver's bid in one click. Optiver is the named other side. Optiver's own explainers describe DCP counterparties as institutions such as pension funds, asset managers, insurers, and sovereign wealth funds.

```text
you need a trade
  |
  +--> lit exchange: public book, visible depth, leakage risk
  |
  +--> dark pool: private match if someone else is there
  |
  +--> internalization / wholesaler: a firm takes the other side
  |
  +--> wholesale RFQ: broker asks MMs for a firm block quote
  |
  +--> DCP: institution streams directly with a named MM
```

Dark pools are attractive when natural opposite flow is already waiting and you want low leakage. Principal routes are attractive when you need the whole amount done, want a firm price, or need someone to warehouse risk. That service usually costs a concession versus mid. Off-exchange is not automatically better than a dark pool, and a dark pool is not automatically better than a lit exchange. Each path solves a different problem.

Venue choice is part of the trade, not an afterthought. It changes what information you reveal, how likely you are to finish, what price you get, and how much the rest of the market can see coming.

## How Block Trades Hit the Tape

A 1 million share print does not mean someone walked a million shares through the displayed book. Large size is often negotiated upstairs, matched in a dark ATS, or facilitated bilaterally. The trade still has to reach the public consolidated tape. Exchange matches report through the exchange. Off-exchange matches report through a FINRA facility: a Trade Reporting Facility (TRF) or the Alternative Display Facility (ADF). Joel Hasbrouck's market-structure notes put the point cleanly: darkness is the absence of a public quote at the trade price, not the absence of a trade report.

What you usually see on the tape is size, price, time, and an off-exchange reporting venue. What you usually do not see is the buyer, the seller, or the specific dark pool or desk that arranged the trade. FINRA later publishes ATS volume aggregates with a lag; that is coarser and slower than the real-time print.

### How big is the delay?

For U.S. NMS stocks during the hours the FINRA facility is open, members must report as soon as practicable, but no later than 10 seconds after execution. That is FINRA's trade-reporting rule, not a folklore estimate. Reports after 10 seconds are marked late. So the legal window is seconds, not minutes. In practice, many prints arrive faster than the outer limit, but execution and dissemination are still two clocks: the market can keep quoting while the block is written up and sent.

That short gap is enough to create a visual puzzle. A block can be agreed when the market was near $100.00, then print a second or two later after the lit book has already moved. The print looks "late" relative to the quotes you are staring at now, even when the firm reported inside the rule.

Important contrast: some futures and non-U.S. venues have historically allowed much longer delayed publication for qualifying blocks. Academic work on reporting delays often studies those regimes. Do not import a one-hour futures delay into U.S. equity tape reading. For U.S. stocks, think seconds.

### Why can a block print below the market?

Yes, it happens. A negotiated print does not have to sit inside the current bid-ask at the moment you see it. Common reasons:

1. **Reporting lag versus live quotes.** The price belonged to an earlier moment. By dissemination time, the lit NBBO may already be higher or lower. Sale-condition codes such as Sold Out of Sequence exist partly for this shape of print.

2. **Prior reference price or stopped stock.** The parties may have agreed a price earlier, or the broker may have guaranteed a price, then executed later. FINRA requires two timestamps for many of these reports: the reference or agreement time, and the execution time. Reg NMS Rule 611 also has exceptions for certain stopped orders and for trades whose price is not based on the contemporaneous quote.

3. **Average-price or derivatively priced prints.** The tape price may be an average across many child fills, or tied to another instrument. That level may never have been the live quote.

4. **Qualified contingent trades and related packages.** Stock legs that are part of a contingent package can print away from the protected quote under specific Rule 611 exemptions when the contingency and hedge conditions are met.

5. **The block never touched the displayed book.** A large off-exchange print adds volume without consuming the lit depth you are watching. So you can see a huge print "through" or below the market while the public book still shows a normal spread, or while the lit book is separately trading down for its own reasons.

```text
block negotiated off-exchange
  -> report to FINRA TRF/ADF within ~10 seconds
  -> SIP disseminates print on consolidated tape
  -> you see size/price/venue code, not counterparty names
  -> lit quotes may already have moved
```

A useful desk habit is to separate three questions: Did size print? Was it on-exchange or off-exchange? Does the sale condition say this price is contemporaneous with the live book, or referenced / averaged / out of sequence? Size alone is a weak screen. Institutions often slice a parent order into many ordinary-looking child prints, and auction crosses can also be large without being upstairs blocks.

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

A large tape print is not proof that the lit book just traded that size. Off-exchange blocks report after the fact, can print outside the live NBBO, and need not consume displayed depth.

## Recap

Orders turn a motive into a claim on liquidity. Market orders demand immediacy; limit orders post price conditions and wait. The lit book stores bids and offers, the spread prices immediacy, and depth tells you how far a given size must walk. Queue priority decides who gets served first at a price. Venues matter because lit, dark, and other off-exchange mechanisms reveal different amounts of information and offer different fill certainty. Large blocks still hit the public tape, usually through a FINRA facility within about 10 seconds, but the print may sit away from the live book because reporting lags quotes, or because the price was referenced, averaged, stopped, or contingent. For flows trading, especially index and rebalance flow, the practical question is never only "what is the price?" It is "what can I actually execute, where, by when, and what will that reveal?"

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

**dark pool**: A private matching venue with no public book like an exchange. A trade happens only if opposite interest is there. The trade still prints afterward.

**alternative trading system (ATS)**: A non-exchange trading venue regulated under rules such as Regulation ATS. Dark pools are usually non-display ATSs.

**off-exchange trading**: Any trade not matched on a registered exchange's public book. Includes dark pools, internalization, wholesale blocks, and DCP.

**retail broker**: The brokerage ordinary investors use to place orders, such as Robinhood, Fidelity, or Schwab.

**market maker**: A firm that quotes buy and sell prices and takes the other side using its own capital. Optiver and Jane Street are examples.

**broker internalization**: Your broker fills your order from its own inventory instead of sending it to an exchange or dark pool.

**wholesaler execution**: A retail broker sends your order to a wholesale market maker, which usually takes the other side as principal.

**wholesale / RFQ block trading**: A broker asks one or more market makers for a firm quote on a large block. One market maker takes the whole risk.

**direct counterparty (DCP) trading**: An institution connects directly to a market maker, gets live two-way prices all day, and trades without a broker in the middle.

**walking the book**: Consuming multiple price levels with one aggressive order because size exceeds depth at the best price.

**consolidated tape**: The public record of U.S. equity trades disseminated through the SIP, including exchange and off-exchange prints.

**Trade Reporting Facility (TRF)**: A FINRA facility used to report off-exchange U.S. equity trades to the tape.

**block trade**: A large negotiated trade, often arranged away from the lit book and later reported as an off-exchange print.

**sale condition**: A code on a tape print that flags how the trade was priced or sequenced, such as prior reference price, average price, or sold out of sequence.

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

8. Why can a 1 million share print appear below the current market?

Off-exchange blocks report after execution, usually within about 10 seconds, while quotes keep moving, and some prints use earlier reference, stop, average, or contingent prices. The print also need not consume the displayed book you are watching.
