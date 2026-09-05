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

Dark pools exist so large traders can search for a match without advertising size on the lit book. They are not a special hedge-fund-only playground, and they are not how a fund "trades itself" instead of using a broker. Most hedge-fund flow still goes to a broker or EMS; the broker's smart order router may rest or ping dark pools, or a large fund may send child orders there directly after becoming a subscriber. Retail usually cannot subscribe. FINRA lists the venues. Common names include Liquidnet, UBS ATS, JPM-X, Goldman Sigma X2, Morgan Stanley MS Pool, Virtu POSIT, Instinet BlockCross, IntelligentCross, and BIDS. JPM-X's Form ATS-N says subscribers must be JPMorgan institutional clients or broker-dealers.

The usual benefit is price improvement versus crossing the spread, plus less pre-trade leakage. If the lit market is $99.98 bid / $100.02 ask, an urgent buy that lifts the offer pays $100.02. A midpoint dark fill is $100.00. Some pools can also match inside the spread at $99.99. That is still the same idea: you paid less than the ask. It is not a special dark-pool discount below fair value. You captured some of the spread instead of giving it all to the displayed seller. If you fill at the ask, you got no improvement. Fill is uncertain. The other side can still be informed.

You cannot see dark liquidity the way you see a lit book. There is no public bid size. Desks infer it. Brokers send small immediate-or-cancel pings; a fill hints someone was there. Some venues use indications of interest or conditional orders: a non-firm "I might have size," then a firm-up if a contra appears. Those methods leak a little information and can be gamed, which is why some pools restrict tiny IOC pings.

An ISO sweep is a lit-market tool, not a dark-pool tool. Under Reg NMS Rule 611, an intermarket sweep order lets a router hit one exchange immediately while also sending orders to clear better protected quotes on other exchanges. Dark pools do not display protected quotations, so you do not ISO-sweep them.

A common sequence for a marketable buy that is not desperate is: ping dark pools first for a midpoint or inside-spread fill, then ISO-sweep displayed size on NYSE, Nasdaq, and the other lit venues if shares remain. Barclays' published U.S. algo FAQ describes that shape as Ping (hidden liquidity at or inside the spread), then Sweep. It is not a law. Urgent flow may skip dark and go straight to the lit book. Some exchange routers hit their own book first. Patient algos may rest in the dark instead of sweeping at all.

A FIX link is the private pipe that carries those orders. FIX, the Financial Information eXchange protocol, is the industry message format. A simplified New Order Single looks like this:

```text
8=FIX.4.2|35=D|11=ORD123|55=XYZ|54=1|38=10000|40=2|44=100.00|
```

`35=D` means new order. `55=XYZ` is the stock. `54=1` is buy. `38=10000` is size. `40=2` is a limit. `44=100.00` is the limit price. Real messages add sender, target, timestamps, and a checksum. JPM-X's materials describe direct access as FIX 4.2. FIX is the language. It is not a venue.

### What "off-exchange" means

Off-exchange simply means the trade was not matched on a registered exchange's public book. Dark pools are one off-exchange path. There are others. The important split is:

- **matching venues**, where you hope another order is already there
- **principal venues**, where a firm takes the other side with its own capital

A firm like Optiver can do both, because market making is a business of taking the other side, not a single venue. On a lit exchange, it posts bids and offers in the public book. Separately, it can take a block or a streamed DCP trade as principal: the client sells to Optiver, Optiver owns the shares, then Optiver hedges by selling futures, ETFs, or stock, including on lit venues. Jane Street and bank dealer desks work the same way. That is optional inventory risk, not a requirement that every order sit on the public book. If the principal trade is off-exchange, it still must be reported to the tape through a FINRA TRF/ADF, usually within 10 seconds. Lit exchange fills print through the exchange as usual.

A retail broker is the firm ordinary investors use to place stock orders, such as Robinhood, Fidelity, or Schwab. An institutional broker helps large funds trade. Those are different businesses from a market maker like Optiver, though they interact constantly.

### Simple scenarios

**1. Dark pool**

A pension fund wants to buy 200,000 shares quietly. Its broker's router sends the order to a dark pool such as Liquidnet, UBS ATS, or JPM-X. If another institution is already selling there, they may match near $100.00 midpoint. If not, nothing happens. The fund did not get a promise that the trade would finish. The print still goes to the tape; the pool name is usually not on the public print.

**2. Broker internalization**

Internalization means the firm that handles your order takes the other side with its own capital, instead of matching you on an exchange. For many big bank brokerages, that can mean an affiliated trading desk.

Example: Merrill Edge / Merrill Lynch is part of Bank of America. Merrill's own disclosures say customer equity orders may be executed with a Merrill equity trading desk as principal, and the confirmation will say Merrill acted as principal. Merrill also says it does not receive payment for order flow from equity liquidity providers the way some discount brokers do. So if your Merrill order is filled by Merrill's desk, that is closer to classic broker/affiliate internalization: you traded with Bank of America's brokerage complex, not with Nasdaq's book.

**3. Wholesaler execution (what Robinhood usually does)**

This is the common path for many retail market orders, and it is not the same as your app broker filling you itself.

Example: You buy 100 shares of XYZ on Robinhood. Robinhood's Rule 606 reports show that non-directed stock orders are largely routed to wholesale market makers such as Citadel Securities, Virtu Americas, Jane Street Capital, and similar firms. Those wholesalers usually take the other side as principal and may pay Robinhood for the order flow. So you did not typically buy "from Robinhood's inventory." You bought from Citadel or Virtu (or another wholesaler), off-exchange, and the trade still prints to the tape afterward.

SEC Rule 606 is the public order-routing report. Brokers must post, each quarter, where they sent non-directed retail-style stock and options orders, and whether they were paid for that flow. That is how we know Robinhood sent a large share of orders to Citadel and Virtu. Schwab and TD Ameritrade sit in a similar retail wholesaler world. Goldman Sachs is different: it is mainly an institutional bank and dealer, not a mass-market Robinhood-style app.

**4. Wholesale block / RFQ**

A pension fund needs to sell 500,000 shares now. Its broker messages several market makers: "Firm quote on 500,000 XYZ?" Optiver, Jane Street, or a bank desk may reply with a two-way price. The broker lifts one offer. That is a block trade in the ordinary desk sense: large size, negotiated away from the lit book, one print. NYSE historically treated 10,000 shares as a "block," but traders usually mean size that is large versus the name's depth, not that legal cutoff.

When is it reported? After the parties agree and the trade is executed, the off-exchange report goes to a FINRA reporting facility as soon as practicable, no later than 10 seconds. You then see a large print. You do not see the RFQ chat.

RFQ means request for quote: the broker asks market makers for a firm price on a stated size. TRF means Trade Reporting Facility: the usual FINRA pipe that takes an off-exchange trade and sends it to the consolidated tape. There are two TRFs today, run with Nasdaq and with NYSE. ADF means Alternative Display Facility: another FINRA facility that can display OTC quotes and report OTC trades in NMS stocks. Most of the large prints you see as "off-exchange" came through a TRF. The ADF is the same job with a different FINRA door. Neither is a dark pool. They are reporting utilities, not matching engines.

Why can that print sit 3% away from the inside market? Sometimes the tape is stale versus live quotes, as the block section below explains. Sometimes the price is honestly worse than the current 100-share bid because 500,000 shares is not the same product as 100 shares. The market maker is taking inventory risk and will have to hedge. Academic upstairs-market work (Keim and Madhavan; Holthausen, Leftwich, and Mayers) finds large blocks often require a concession, and seller-initiated blocks often have a temporary markdown. Three percent is large for a liquid large-cap name and more plausible in a thinner stock, a rushed sale, or a print that is referenced, averaged, or contingent rather than a clean cash print at the live NBBO.

**5. Direct counterparty (DCP)**

"Continuous" here means a live two-way quote that stays up all day, not a stream of customer orders and not a public WebSocket anyone can join. Optiver refreshes a bid and an ask in size into the institution's EMS, meaning its execution management system: the trading screen and software the fund uses to send orders (examples are Bloomberg EMSX, FlexTrade, or a house-built blotter). When the fund wants to trade, it hits or lifts that quote. The plumbing is a private electronic link, often FIX; WebSocket is possible as a transport, but the point is the relationship, not the protocol.

This is allowed. It is ordinary bilateral OTC trading between two broker-dealers or a broker-dealer and an institution. When they trade, that execution is reported to the tape like other off-exchange trades. The streaming quotes themselves are not public and do not print. Only the completed trade prints.

### When a fund uses a dark pool versus DCP

Optiver is not a fund. It is a market maker. A pension fund or hedge fund is the client choosing a path. Optiver is often the firm on the other side of DCP or RFQ.

Use a dark pool when you hope natural opposite interest is already there, you can wait, and you want a chance at midpoint or $99.99-style improvement without showing size. Nobody promises you a fill. You are matching, not hiring a dealer.

Use DCP (or an RFQ block) when you need size now and a firm price from a named market maker. Optiver's own explainers say DCP is for institutions that want continuous streamed size they can hit, with less pre-trade book impact and more price certainty. You usually pay a concession versus mid because Optiver is warehousing the risk. RFQ is the one-off version of that ask.

A fund does not pick one forever. A rebalance algorithm may ping dark all afternoon, then RFQ or DCP a leftover block into the close.

What Optiver itself does: it provides DCP and answers RFQs. That is its principal business with institutions. It also quotes on lit exchanges. When Optiver needs to hedge the inventory it just bought from a fund, it may route like anyone else, including dark pings and lit sweeps. The fund uses dark to hunt for a silent match. Optiver uses DCP to stand in as the match when the fund does not want to hunt.

Worked path for a fund buying 50,000 shares with bid $99.98 / ask $100.02:

```text
patient buy
  -> ping dark: maybe fill at $100.00 mid or $99.99 inside the spread
  -> leftover shares
  -> ISO sweep lit books at $100.02 and worse if needed

need the whole block now
  -> RFQ or DCP: Optiver (or another MM) is the other side
  -> firm size, likely worse than mid
  -> Optiver hedges on lit / dark / futures
```

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

**RFQ (request for quote)**: Asking one or more market makers for a firm price on a stated size, usually a block.

**wholesale / RFQ block trading**: A broker asks one or more market makers for a firm quote on a large block. One market maker takes the whole risk.

**direct counterparty (DCP) trading**: An institution connects directly to a market maker, gets live two-way prices all day, and trades without a broker in the middle.

**EMS (execution management system)**: The software a fund uses to see prices and send orders. The DCP stream shows up there.

**FIX (Financial Information eXchange)**: The standard electronic message protocol funds, brokers, and venues use to send orders, cancels, and fills. A FIX link is that private connection.

**midpoint**: The price halfway between the best bid and best ask. Many dark fills occur here, which is price improvement versus lifting the offer or hitting the bid.

**ISO (intermarket sweep order)**: A Reg NMS order type that lets a router execute on one lit venue immediately while also sending orders to clear better protected quotes on other lit venues. Dark pools do not have protected quotes, so they are not ISO-swept.

**indication of interest (IOI) / conditional order**: A non-firm signal that size may be available in the dark. A match invitation can then ask the sender to firm up. Not a public book.

**walking the book**: Consuming multiple price levels with one aggressive order because size exceeds depth at the best price.

**consolidated tape**: The public record of U.S. equity trades disseminated through the SIP, including exchange and off-exchange prints.

**Trade Reporting Facility (TRF)**: A FINRA facility that accepts off-exchange U.S. equity trade reports and sends them to the public tape. Most dark-pool, internalized, and upstairs prints go this way.

**Alternative Display Facility (ADF)**: Another FINRA facility for OTC quoting and trade reporting in NMS stocks. Same idea as a TRF: a reporting door, not a matching venue.

**block trade**: A large negotiated trade, often arranged away from the lit book and later reported as an off-exchange print.

**sale condition**: A code on a tape print that flags how the trade was priced or sequenced, such as prior reference price, average price, or sold out of sequence.

**Rule 606**: The SEC rule that makes brokers publish quarterly reports on where they routed non-directed customer orders and whether they were paid for that flow.

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

9. When would a fund use a dark pool instead of DCP with Optiver?

Dark pool: hunt for a silent match and maybe buy at $100.00 or $99.99 instead of $100.02; fill is not guaranteed. DCP: Optiver is the named other side with a firm streamed size; you pay for certainty, and Optiver is a market maker, not the fund.
