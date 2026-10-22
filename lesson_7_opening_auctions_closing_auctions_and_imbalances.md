# Lesson 7: Opening Auctions, Closing Auctions, and Imbalances

## Learning Goal

Many important trades do not happen as a stream of small continuous-market fills. They happen in auctions, especially at the open and close.

This matters for index mechanics because portfolios, funds, and benchmarks often use official opening or closing prices. If a fund is judged against the closing price, trading throughout the day creates tracking error. Trading in the closing auction gives the fund the same price the benchmark uses. That is why a large amount of benchmarked and index-related flow concentrates near the close.

## The Problem: Everyone Wants the Same Timestamp

Suppose an index fund must buy 1,000,000 shares of XYZ after an index rebalance. The index will value XYZ at the official closing price. The fund's investors will see net asset value, or NAV, based on that same close.

If the fund buys at 2:00 p.m. at $99.80 and XYZ closes at $100.20, it may have traded well economically, but it did not match the benchmark. If it buys in the closing auction at $100.20, it has no slippage versus the official benchmark price. That is tracking-error logic, not a valuation view.

```text
benchmark uses official close
  -> fund wants official close
  -> orders concentrate in closing auction
  -> imbalance reveals how much buy or sell interest is left
```

The close matters because the close is the accounting and benchmark timestamp.

## What an Auction Is Trying to Solve

Continuous trading matches orders one at a time. A buy market order walks the ask. A seller who arrives one second later may miss that buyer.

An auction pauses that sequence and batches interest. Buy and sell orders are collected, then the exchange picks one price that matches as many shares as possible under its rules. Everyone who participates in that match trades at the auction price.

That is useful when many investors want the same reference price. Instead of racing through the book at 3:59:59, they can submit auction orders and meet at one clearing price.

```text
continuous market
  order meets book immediately

auction
  collect interest
  calculate clearing price
  print one official auction price
```

The auction does not make supply and demand disappear. It concentrates them and makes the clearing problem explicit.

## A Small Worked Example

XYZ last traded at $100.00. Just before the close it has this auction interest:

```text
buy MOC:   700,000 shares   (any price)
buy LOC:   200,000 shares   only at $100.10 or lower
sell MOC:  500,000 shares   (any price)
sell LOC:  100,000 shares   only at $100.00 or higher
sell LOC:  200,000 shares   only at $100.08 or higher
```

The exchange tries candidate prices and counts how many shares could trade at each one:

```text
price     buyers    sellers   matched   left over
$100.00   900,000   600,000   600,000   300,000 buy
$100.08   900,000   800,000   800,000   100,000 buy
$100.11   700,000   800,000   700,000   100,000 sell
```

At $100.00 there is a 300,000-share buy imbalance. Raising the price to $100.08 pulls in the second LOC seller, so 800,000 shares can match. Going above $100.10 drops the LOC buyer and matches fewer. The auction picks the price that matches the most shares, so it clears near $100.08. Nasdaq, for example, maximizes matched shares first, then minimizes the leftover imbalance, then stays close to the prevailing quote. The 100,000 shares left over come from the LOC buyer, because MOC orders fill first.

The excess buy demand pushed the closing price eight cents above the last trade, because higher prices were needed to bring in sellers. If an offsetting seller had added 300,000 shares at $100.00, all 900,000 shares to buy would have matched at $100.00 and the price would not have needed to rise. That is the same supply-and-demand logic as earlier lessons, but with a public clock and a public batch.

## Order Types: MOC, LOC, and Imbalance Orders

A market-on-close order, or MOC, says: trade me in the closing auction at the auction price. It cares about completion at the close, not a limit price.

A limit-on-close order, or LOC, says: trade me in the closing auction, but only if the auction price is no worse than my limit.

Imbalance-only orders are meant to offset auction imbalances. Nasdaq calls its version imbalance-only (IO) orders and describes them as liquidity-providing orders that stabilize the crossing price. NYSE's version is the Closing Offset order, which "executes only against the opposite side of an imbalance; never adds to an imbalance." In both cases the order can only supply the side the auction is short of.

```text
MOC -> must trade at the close
LOC -> trade at the close if price is acceptable
IO / offset -> provide liquidity against imbalance
```

The details differ by venue. For desk intuition, focus on the incentives: who must finish, who has a price limit, and who is waiting to provide liquidity if the imbalance is attractive.

**Why not just leave a regular limit order in the book?** Because a regular limit order can fill at any moment during the day. An index fund that leaves "buy 1,000,000 XYZ at $100.10" in the book at noon may be filled at 12:05 at $100.10, and the stock may close at $99.50. The fund wanted the closing price, not just a price below $100.10. An on-close order waits. It does nothing during the day and can only trade in the closing auction, at the single closing price. MOC adds that the order should fill whatever that price is. LOC adds a price limit. A regular limit order still resting at 4:00 does join the cross, but only if nobody filled it first.

On-close orders also show up in the imbalance publication from 3:50, so other traders can see them and respond. A large buyer who hides in the regular book gets no help from offsetting sellers.

**Do they always fill?** Not all of them, and the rules decide who misses. The auction fills orders in roughly this order:

```text
1. MOC orders                         -> any price, so they go first
2. limit orders (LOC or book) priced  -> better than the clearing price
3. limit orders exactly at the price  -> may be partly filled
4. imbalance-only / closing offset    -> only to fill what is left
```

The NYSE Closing Offset order "yields to all other interest in closing auction," which is step 4. In the worked example, the auction cleared at $100.08 with 100,000 buy shares left over. The MOC buyers filled in full, and the LOC buyer with a $100.10 limit got only part of its order. In the Nasdaq example, the LOC seller at $10.10 got nothing because the auction printed at $10.00. An LOC is never filled at a worse price than its limit; it just risks not trading. That is the trade-off: MOC guarantees you trade at the close but not the price, and LOC guarantees the price but not that you trade.

An MOC can occasionally miss as well. If an imbalance is too large to clear within the exchange's price limits, part of the MOC side can be left unfilled. In ordinary closes this is rare, because offsetting liquidity arrives.

## Imbalance Messages

An imbalance is the unmatched buy or sell interest at a reference price. In the worked example, the imbalance at the $100.00 reference price is 300,000 shares to buy.

Exchanges publish auction information so traders can react. Nasdaq's Net Order Imbalance Indicator (NOII) starts at 3:50 p.m. and updates every 10 seconds, then every second from 3:55 p.m. It shows paired shares, imbalance size and side, and the reference price. From 3:55 p.m. it adds an indicative clearing price, the price the auction would print if it ran at that moment. In the example, that is $100.08. NYSE publishes similar fields every second from 3:50 p.m. They include paired and unpaired quantity, total imbalance, and indicative prices.

Exchanges also set limits on how far the auction price can move. An auction collar is a price band around a reference price. If the clearing price would land outside it, the exchange caps the price or uses special handling instead of printing. This stops one oversized or mistaken order from setting an official close far from where the stock was trading. Nasdaq also limits how aggressive a late LOC can be: an LOC entered after 3:55 p.m. is repriced if its limit is more aggressive than the published reference prices.

This transparency is meant to attract liquidity. If a buy imbalance is public, sellers can choose to join the auction. If the imbalance is large enough, prices may move before the auction because traders anticipate the clearing price.

## Reading an Imbalance Message

An imbalance message answers one question: if the auction ran right now, what would happen? It does that with a handful of numbers. Each one is easier to read once you know what it measures. The examples below use the XYZ auction from the worked example: 900,000 shares to buy and, at $100.00, 600,000 shares to sell.

**Quote.** The best bid and offer in the regular, continuous market at that moment, such as $99.99 x $100.00. It is not part of the auction itself. It matters because Nasdaq picks the reference price from inside it.

**Reference price.** The price at which the exchange counts the auction. Two numbers in the message are measured at it: paired shares (how many would match at this price) and the imbalance (how many are left over, and on which side). Nasdaq's Closing Cross FAQ defines paired shares as on-close shares Nasdaq "is able to pair off at the current reference price." It defines the imbalance as closing shares "seeking additional liquidity at the current reference price." NYSE's imbalance feed spec likewise defines its paired quantity as shares "paired off at the Reference Price." Without a fixed price, "the imbalance" would mean nothing, because the count changes with price. At $100.00 in the worked example, the imbalance is 300,000 shares to buy. At $100.08 it is only 100,000, because a higher price brings in another seller. Nasdaq also uses the 3:50 and 3:55 reference prices to cap late LOC orders: an LOC entered after 3:55 is repriced if its limit is more aggressive than either one. The near and far prices are not measured at the reference price. They are separate answers to a different question: where would the price have to go to clear?

Nasdaq only considers prices from the bid to the offer, inclusive, so the yardstick stays close to where the stock trades now. Among those prices, it picks the one that pairs the most shares. If two prices tie, it picks the one with the smaller imbalance, and after that the one closest to the midpoint.

*Example:* XYZ is quoted $99.99 x $100.00, so with one-cent ticks the only candidates are $99.99 and $100.00. Count the auction orders at each:

```text
price    buyers    sellers                            paired
$99.99   900,000   500,000  (MOC sellers only)        500,000
$100.00  900,000   600,000  (+ LOC seller at $100.00) 600,000
```

$100.00 pairs more shares, so it wins. The LOC seller who wants at least $100.00 counts only at $100.00. The general pattern is that when buyers outnumber sellers, a higher price can only bring in more sellers. Buyers are the side in excess, so losing a few of them never reduces the paired count. The rule therefore pushes the reference price to the top of the allowed range, which is the offer. With more sellers than buyers, it goes to the bid.

**Paired shares.** How many shares could be matched buyer-to-seller at the reference price. *Example:* at $100.00, 900,000 shares want to buy and 600,000 want to sell. Only 600,000 can be matched, so paired shares = 600,000.

**Imbalance quantity and side.** The shares left over at the reference price, and which side they are on. *Example:* 900,000 − 600,000 = 300,000 left over on the buy side. The message shows imbalance BUY 300,000. This is the number traders watch most closely. It is the forced demand still looking for the other side.

**Far price.** The price at which the auction would clear using only auction orders: MOC, LOC, and imbalance-only orders. It ignores the regular order book. *Example:* in the worked example, auction orders alone clear at $100.08, where the second LOC seller joins. The far price is $100.08.

**Near price.** The price at which the auction would clear if it ran now, also counting limit orders resting in the regular book. *Example:* suppose sellers in the regular book are offering 150,000 shares between $100.01 and $100.05. They take some of the imbalance before the price reaches $100.08, so the near price might be $100.05.

**Near and far do not use the reference price.** Paired shares and the imbalance are counted at the reference price. Near and far are not. Each is found by searching all prices for the one that matches the most shares, and that price can be well outside the current quote. The reference price says how lopsided the auction is at today's price. Near and far say where the price would have to go to clear it. In the Nasdaq example at 3:55, the reference price is $10.15 while near is $10.25 and far is $10.50.

**Both are estimates, not promises.** Near and far are indicative prices: the exchange's live guess at where the closing auction will print, recalculated with every update until 4:00. The near price is the better forecast of the actual close, but it can shift. Limit orders in the regular book can be canceled at any moment, and new ones can arrive. The far price is not fixed either. Locked MOC and LOC orders cannot leave, but new offsetting orders can still arrive and pull it back toward the reference price, as the Nasdaq example below shows. Only the 4:00 print is final.

**Why does the book count at all?** Because ordinary limit orders still resting in the book at 4:00 do trade in the closing cross. Nasdaq says continuous-market orders "will be included in the auction and will be available for execution." NYSE's continuous-book clearing price exists for the same reason. A seller offering 10,000 shares at $100.03 in the regular book at 3:59 is, in effect, also offering them to the auction.

The difference is commitment. After 3:50, MOC and LOC orders are locked: they cannot be canceled or changed. Book orders are not locked. Their owners can cancel them at 3:59:59, and new ones can arrive. So the exchange publishes two prices:

```text
far price    counts only locked-in auction orders
             -> where the close lands if the book contributes nothing

near price   also counts what is resting in the book right now
             -> where the close lands if nothing changes before 4:00
```

The near price is the better forecast of the print. The far price is the more conservative one. The gap between them tells you how much the close depends on liquidity that could still disappear. If the far price is well above the near price, the auction is leaning on book sellers. If those sellers cancel before 4:00, perhaps because they also see the imbalance and want a better price, the close moves toward the far price.

NYSE uses different names for similar numbers. Its **paired quantity** and **total imbalance** mean the same as Nasdaq's paired shares and imbalance. Its **closing-only clearing price** works like Nasdaq's far price, and its **continuous-book clearing price** works like the near price.

```text
reference price   the yardstick: roughly where the stock trades now
paired            shares that would match at the reference price
imbalance         shares left over at the reference price, and which side
far / closing-only     clearing price from auction orders alone
near / continuous-book clearing price if the cross ran now, book included
```

## Two Closes, Message by Message

**A Nasdaq close.** Nasdaq's Closing Cross FAQ publishes this example. The stock trades around $10. Read each snapshot, then the note under it.

```text
3:50 p.m.  quote $9.99 x $10.00
           paired 4,000 | imbalance BUY 500 | reference $10.00
```

*What you are seeing:* the first NOII of the day. At $10.00, 4,500 shares want to buy in the close and 4,000 want to sell. So 4,000 pair and 500 buy shares are left over. The reference price is the $10.00 offer because buyers outnumber sellers. Near and far prices are blank because Nasdaq publishes them only from 3:55.

```text
3:55 p.m.  quote $10.10 x $10.15
           a buy 500 MOC arrives just before the MOC cutoff
           paired 4,000 | imbalance BUY 1,000 | reference $10.15
           near $10.25 | far $10.50
```

*What you are seeing:* the regular market has moved up to $10.10 x $10.15, so the reference price moves to the new offer, $10.15. A late 500-share MOC buyer doubles the imbalance to 1,000. Now the indicative prices appear. If the cross ran now, it would print at $10.25 (near), using sellers resting in the book. Without the book, auction orders alone would need $10.50 (far). The message is saying there is not enough selling in the auction, and the price would have to rise a lot to find it. That is the invitation to sellers.

```text
3:56-3:59  three sellers respond:
             sell 1,000 IO  at $9.95
             sell 1,000 LOC at $10.10
             sell 1,000 LOC at $10.00
           paired 5,000 | imbalance 0 | near $10.00 | far $10.00
```

*What you are seeing:* the imbalance attracted 3,000 shares of offsetting sell interest, three times what was needed. All 5,000 buy shares can now be matched, so the imbalance is zero. Because a seller will sell at $10.00, the auction no longer has to rise to find sellers. Near and far both drop to $10.00. The publication did its job: it showed sellers an opportunity, and they came.

```text
4:00 p.m.  quote $10.00 x $10.15
           closing cross prints 5,000 at $10.00
```

*What you are seeing:* the cross runs at $10.00, and only the $10.00 LOC seller fills. The $10.10 LOC asked for more than the clearing price, so it gets nothing. The IO order is the surprising one. Its seller said "$9.95 or higher," and the cross printed at $10.00, so it looks as if it should have filled. It did not, because of a Nasdaq rule. IO orders "priced more aggressively than the 4:00 p.m. Nasdaq bid (or ask) will be adjusted to the Nasdaq bid (or ask)" before the cross runs.

For a sell order, more aggressive means willing to sell cheaper. At 4:00 the regular-market quote is $10.00 x $10.15, so the best offer is $10.15. The IO's $9.95 is cheaper than that, so Nasdaq raises it to $10.15. The order now effectively says "sell only at $10.15 or higher." The cross prints at $10.00, which is below $10.15, so the IO does not trade.

```text
IO entered:        sell 1,000 at $9.95
4:00 Nasdaq offer: $10.15
IO repriced to:    sell 1,000 at $10.15   (cannot sell below the offer)
cross price:       $10.00                 -> $10.00 < $10.15, no fill
```

The reason for the rule is the IO's job. An IO is there to absorb an imbalance, not to undercut the market. Capping it at the offer means IO sellers can never push the close below where the regular market is offering stock. The cost is that an IO seller cannot win by offering a lower price. The LOC seller at $10.00 could, so the LOC got the fill. Nasdaq's point is that an LOC can offset an imbalance at a better price than an IO can.

So IO and LOC suit different sellers. An IO suits a seller who wants to sell only at or above the market's offer, as a paid liquidity provider. A seller who actually wants to trade, and will take a lower price to do it, should use an LOC.

The rule also affects how to read the 3:59 message. An IO's effective price is not known until 4:00, when the final quote sets it. At 3:59, IO sellers can make the imbalance look covered and still contribute nothing at the cross if the final offer sits above the clearing price. A desk watching the imbalance should ask what kind of order is offsetting it, not only how many shares.

**An NYSE close.** NYSE lists its fields but does not publish an example with numbers. This one is stylized and uses the XYZ auction from the worked example.

```text
3:50:00  MOC/LOC cutoff
         paired 600,000 | total imbalance BUY 300,000 | reference $100.00
         closing-only price $100.08 | continuous-book price $100.05
```

*What you are seeing:* the cutoff has frozen the forced flow, and NYSE publishes it. At $100.00, 300,000 shares to buy have no seller. Auction orders alone would clear at $100.08. Counting sellers resting in the regular book, the auction would clear at $100.05. A trader reads this as roughly 300,000 shares of buying to absorb, about 5 to 8 cents of upside to sell into, and ten minutes to decide.

```text
3:50:01 onward  updates every second if anything changed
                only sell orders (the side that offsets the imbalance) are accepted
```

*What you are seeing:* NYSE locks the side that caused the imbalance. Nobody can add more buying in the auction now, so the 300,000 figure can only shrink.

```text
3:56:12  a sell LOC for 300,000 at $100.00 arrives
         paired 900,000 | total imbalance 0
         closing-only price $100.00 | continuous-book price $100.00
```

*What you are seeing:* one large seller, perhaps a market maker or an event trader who bought earlier, fills the whole gap at $100.00. The imbalance is zero, and both clearing prices fall back to $100.00.

```text
4:00:00  closing auction prints 900,000 at $100.00
```

*What you are seeing:* the forced buyers got their shares at the official close, which is what their benchmark uses. The seller earned the right to supply 300,000 shares in one print. Whether that was a good trade depends on where XYZ opens tomorrow.

Real NYSE messages carry more fields, such as the auction collars and the side of any unpaired shares. The sequence is the same, though: the cutoff freezes the forced flow, the feed publishes it, and offsetting liquidity has ten minutes to respond.

**Other exchanges.** The official close for a stock comes from the auction on its listing exchange. NYSE closes NYSE-listed stocks, Nasdaq closes Nasdaq-listed stocks, NYSE Arca closes many ETFs, and Cboe BZX closes its own listings. Their clocks differ:

```text
exchange     imbalance data starts      MOC cutoff     LOC cutoff
NYSE         3:50, every 1 sec          3:50           3:50 (offsetting only after)
Nasdaq       3:50 every 10 sec,         3:55           3:58 (IO until 4:00)
             3:55 every 1 sec
Cboe BZX     3:00 every 5 sec,          3:55           3:59
             3:59 every 1 sec
NYSE Arca    (not checked)              3:59           3:59
```

These times change. Until April 2019, NYSE's MOC/LOC cutoff and its first imbalance publication were at 3:45 p.m., not 3:50. BZX moved its MOC cutoff from 3:59 to 3:55 in 2025. Check the current exchange notice before relying on any clock.

Raw messages are available too. Nasdaq posts sample TotalView-ITCH files that include NOII messages, and vendors such as Databento sell historical NYSE and Nasdaq imbalance data.

## Why the Close Is So Important

The close is the price used by many portfolios, funds, and benchmarks. Mutual fund NAVs are commonly struck from closing prices. Index levels use official closes. Performance reports compare managers to closing-price benchmarks.

That creates a mechanical incentive. If you are judged against the close, you want to trade at the close. State Street Global Advisors describes this as a structural reason passive funds and ETFs concentrate activity in the closing auction. Academic work on closing auctions similarly finds that passive ownership and ETF ownership are strongly associated with auction volume, and that auction volume spikes on index rebalancing days, option expiration days, and month-end days.

This does not mean every closing-auction order is passive. It means the close attracts flow from participants whose benchmark is the close.

## Why Imbalances Move Prices

An imbalance is a supply-and-demand signal with a deadline.

If a stock shows a large buy imbalance at 3:50 p.m., the market learns that more buyers than sellers want the auction. Sellers can demand a higher price. Event traders can buy before the close and offer shares into the auction. Dealers can decide whether the concession is enough to warehouse the other side.

```text
large buy imbalance
  -> market expects auction demand
  -> sellers require a higher price
  -> pre-close price may rise
  -> auction clears where enough sell interest appears
```

This connects to Lesson 6. A liquidity provider usually takes the other side of a closing imbalance more readily than an anonymous sweep, because much imbalance flow is mechanical. An index fund buying because of a rebalance is not trading on a view of the company. The liquidity provider still wants a concession for the inventory it takes on, which is the risk Lesson 5 described. It wants a larger one when the imbalance might reflect news.

The price move can be temporary. Once the closing benchmark trade is done, the forced demand may disappear. But it can also persist if the auction revealed real information or if indexers permanently changed holdings.

## Opening Auctions Versus Closing Auctions

The opening auction solves a different problem. Overnight news accumulates while the market is closed. The open has to turn that news, pre-market orders, and liquidity into a first regular-session price.

The close is less about overnight information and more about a benchmark timestamp. The market has traded all day, but many investors still need the official final print.

```text
open
  -> digest overnight information
  -> set first regular-session price

close
  -> concentrate benchmark and NAV flow
  -> set official end-of-day price
```

Both auctions batch orders. The reason people care about each one is different.

## What Can Go Wrong

Too much one-sided flow can overwhelm natural liquidity. The auction clears, but at a large concession.

Traders can crowd the imbalance. If everyone sees the same buy imbalance and buys ahead of it, the forced buyer pays earlier and more expensively.

Liquidity providers can step away. If the imbalance is large, volatile, or information-sensitive, dealers may demand a wider concession or less size.

Operational rules matter. On both NYSE and Nasdaq, orders on the close cannot be canceled or changed after 3:50 p.m. A wrong order entered at 3:49 p.m. may be impossible to fix by 3:51 p.m. The cutoffs in the table above decide what a trader can still do in the last ten minutes.

## Common Misconceptions

The closing auction is not automatically cheap. It can be deep, but if everyone wants the same side, depth comes at a worse price.

The imbalance is not a guaranteed forecast. It changes as new orders arrive, and it can attract offsetting liquidity.

MOC is not a price-control order. It is a completion-at-the-close order. If you care about price limits, that is what LOC is for.

The open and close are not the same event. The open digests news. The close concentrates benchmark, NAV, rebalance, and hedging flow.

## Recap

Auctions batch orders and clear them at a single official price. The opening auction turns overnight information into the first regular-session price. The closing auction is central to benchmarked trading because many portfolios, NAVs, and indexes use the official close. MOC orders demand completion at the auction price; LOC orders add a price limit; imbalance-only or offsetting orders provide liquidity against the imbalance. Imbalance feeds reveal unmatched buy or sell interest, which can attract liquidity but also move prices when the flow is large and urgent. For index trading, the close matters because tracking error is measured against that timestamp.

## New Terms

**auction**: A trading mechanism that batches buy and sell interest and clears at a single price.

**opening auction**: The auction that sets the first regular-session price after overnight information and pre-open orders.

**closing auction**: The auction that sets the official end-of-day price.

**market-on-close (MOC)**: An order to trade in the closing auction at the auction price.

**limit-on-close (LOC)**: An order to trade in the closing auction only if the auction price satisfies a limit.

**imbalance**: The unmatched buy or sell quantity at a reference or indicative price.

**indicative match price**: An exchange-published estimate of the auction price that would maximize executable volume under the rules at that moment.

**paired quantity / matched volume**: Shares that can currently be matched in the auction.

**reference price**: The price an imbalance message uses to count paired shares and the imbalance. On Nasdaq, it is chosen from inside the current quote.

**far price / closing-only clearing price**: The price at which the auction would clear using only auction orders.

**near price / continuous-book clearing price**: The price at which the auction would clear if it ran now, counting limit orders resting in the regular book as well.

**auction collar**: A price boundary limiting where the auction can execute.

**tracking error**: Difference between a fund's return and its benchmark return.

## Questions to Test Yourself

1. Why do many index funds and benchmarked managers trade near the close?

Their benchmarks and NAVs use official closing prices. Trading in the closing auction reduces slippage versus that benchmark timestamp.

2. What is the closing auction trying to solve?

It batches many orders that want the same official end-of-day price. The auction finds one clearing price where buy and sell interest can match.

3. Why can auction imbalances move prices?

A large imbalance tells the market that one side still needs liquidity by a deadline. The opposite side can demand a price concession, and other traders may position ahead of the auction.

4. What can go wrong if too much flow concentrates in the auction?

The auction can clear far from pre-auction prices, and everyone benchmarked to the close may crowd the same side. Operational cutoffs can also make errors hard to fix.

5. How does benchmark tracking affect execution timing?

A fund judged against the close takes on tracking risk whenever it trades at any other time, so it pushes its trading into the closing auction. That timing is predictable, which is why other traders can position ahead of the imbalance.

## Sources

NYSE. "Auctions." https://www.nyse.com/auctions

NYSE. "NYSE Opening and Closing Auctions Fact Sheet." https://www.nyse.com/publicdocs/nyse/markets/nyse/NYSE_Opening_and_Closing_Auctions_Fact_Sheet.pdf

SEC. NYSE Rule 7.35 / 7.35B auction imbalance rule materials. https://www.sec.gov/files/rules/sro/nyse/2024/34-100327.pdf

Nasdaq. "The Nasdaq Opening and Closing Crosses." https://nasdaqtrader.com/content/productsservices/trading/crosses/openclose_faqs.pdf

Nasdaq. "Nasdaq Closing Cross FAQ." https://www.nasdaqtrader.com/content/productsservices/Trading/ClosingCrossfaq.pdf

Nasdaq. "NOIView Specification." https://nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/NOIViewSpecification.pdf

State Street Global Advisors. "Closing time: How passive investing is reshaping equity market microstructure." https://www.ssga.com/sg/en/institutional/insights/how-passive-investing-reshaping-microstructure

Hendershott, Terrence, Dmitry Livdan, and Dominik Roesler. "Who trades at the close? Implications for price discovery and liquidity." *Journal of Financial Markets*. https://www.sciencedirect.com/science/article/abs/pii/S1386418123000502

SEC. 2019. Order approving NYSE's move of the MOC/LOC cutoff from 3:45 p.m. to 3:50 p.m. https://www.federalregister.gov/documents/2019/02/06/2019-01175/self-regulatory-organizations-new-york-stock-exchange-llc-order-approving-a-proposed-rule-change-to

Cboe. 2025. BZX closing auction cutoff changes (Federal Register 2025-08114). https://public-inspection.federalregister.gov/2025-08114.pdf

Cboe. 2023. Filing comparing closing auction cutoffs across exchanges, including NYSE Arca. https://sec.gov/files/rules/sro/cboebzx/2023/34-96861.pdf

NYSE. "XDP Imbalances Feed Client Specification." https://www.nyse.com/publicdocs/nyse/data/XDP_Imbalances_Feed_Client_Specification_v2.2c.pdf
