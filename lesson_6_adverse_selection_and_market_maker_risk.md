# Lesson 6: Adverse Selection and Market Maker Risk

## Learning Goal

Lesson 5 explained inventory risk: the dealer buys from a client, holds a position, and can lose money if price moves before the position is sold or hedged. This lesson explains a different danger: the dealer may be trading with someone who knows more.

Adverse selection means you get picked off by better-informed flow. You sell to the buyer right before good news, or you buy from the seller right before bad news. The trade looks profitable when you collect the spread. Then the fair value moves against you.

## The Problem: The Bad Fill

A market maker quotes XYZ at $99.95 bid and $100.05 ask. A buyer lifts 10,000 shares at $100.05.

If the buyer is a pension fund buying because of a rebalance, the fill may be fine. The market maker is short 10,000 shares, but the trade itself does not reveal a better estimate of value.

If the buyer knows a takeover headline is about to hit, the fill is dangerous. The market maker sold at $100.05 right before the stock's fair value jumped to $103. The five-cent spread did not compensate for a three-dollar information loss.

```text
market maker sells at $100.05
  |
  +--> benign buyer: ordinary liquidity demand
  |
  +--> informed buyer: price should be higher
```

The hard part is that both buyers can look identical in the order book.

## A Small Worked Example

XYZ is quoted $99.95 / $100.05. The market maker sells 10,000 shares at $100.05.

**Case A - uninformed flow.** The buyer is an index fund finishing a benchmark trade. Ten minutes later XYZ is still $100.00. The market maker buys back at $100.00. The trade made about five cents per share before fees and hedge noise.

**Case B - informed flow.** The buyer has better information. Ten minutes later good news is public and XYZ is $103.00. The market maker buys back at $103.00. The trade lost about $2.95 per share.

The same quote produced two very different outcomes. The difference was not size. It was information.

```text
sell 10,000 at $100.05
  benign flow   -> buy back near $100.00 -> spread earned
  informed flow -> buy back near $103.00 -> spread overwhelmed
```

That is why liquidity providers care about the type of flow, not only the number of shares.

## Why Selling to an Informed Buyer Is Dangerous

An informed buyer is not just demanding liquidity. They are telling you, through their trade, that your price may be too low.

Glosten and Milgrom (1985) model this with a specialist who sees orders but does not know whether each trader is informed. A buy order is more likely when the asset is worth more. A sell order is more likely when the asset is worth less. The market maker must protect itself by setting the ask above the expected value conditional on a buy and the bid below the expected value conditional on a sell.

Plainly: after someone buys from you, the asset is a little more likely to be worth more than you thought. After someone sells to you, it is a little more likely to be worth less. The spread is compensation for that possibility.

Kyle (1985) gives a different version of the same problem. An informed trader breaks up orders and hides inside noise trading. The market maker sees net order flow and updates price gradually. Prices move because order flow is informative.

This is why the phrase "orders forecast prices" is useful. The order may not mechanically shove the price. It may reveal that the price was stale.

## Why Spreads Widen When Uncertainty Rises

A spread has to pay for several things: inventory risk, operating cost, competition, and adverse selection. Lesson 5 focused on inventory. This lesson focuses on the informed-trader tax.

Suppose earnings come out in five minutes. The market maker does not know the number. Some traders may know or infer more. If the market maker keeps quoting a tight $99.95 / $100.05 market, informed traders have a cheap option: buy from the stale ask if the news is good, sell to the stale bid if the news is bad.

The rational response is to widen or reduce size.

```text
more uncertainty about true value
  -> higher chance the next trader is informed
  -> bigger expected loss to informed flow
  -> wider spread or smaller quote size
```

This is not cowardice. It is the price of immediacy when the other side may know more.

## Toxic Flow

Toxic flow is order flow that is likely to lose money for the liquidity provider after the trade. The word sounds dramatic, but the idea is simple: the fills you receive are biased toward moments when your quote is wrong.

Practitioners often describe adverse selection as the tendency for passive orders to fill quickly when you wish they had not, and not fill when you wish they had. If your bid fills right before the price falls, that was a bad fill. If your bid sits unfilled right before the price rises, you missed the good fill.

Easley, O'Hara, and coauthors developed models such as PIN, the probability of informed trading, to estimate how much order flow may be information-based. Later high-frequency work such as VPIN tried to measure flow toxicity from volume imbalance. These measures are imperfect. They can confuse high turnover or mechanical flow with private information. The useful desk intuition is still durable: the market maker wants to distinguish ordinary liquidity demand from flow that predicts the next price move.

## What a Market Maker Can See About the Other Side

Sorting benign flow from toxic flow would be easy if the market maker knew who was trading. In US equities and options, the screen usually hides that. Most of what a market maker learns about the other side comes from patterns and labels, not names.

**Equities on a lit exchange.** Exchange direct feeds show each resting order's price, size, side, and an order ID, but usually not the firm. Nasdaq lets a firm attach its market participant ID (MPID) to an order. Its TotalView feed then sends that order as a separate "Add Order with MPID Attribution" message, but most orders go unattributed. When your quote fills, your execution report gives you the price and size, not the counterparty. Clearing does not reveal it either: NSCC steps in as the central counterparty, so your trade settles against the clearinghouse.

**What a print looks like on the tape.** The consolidated tape (the SIP) shows every trade, but each print carries only a few fields. Here is a stylized example:

```text
time          symbol  price    size  venue            conditions
10:31:05.123  XYZ     100.05    300  P  NYSE Arca     @ F
10:31:05.123  XYZ     100.05    400  Q  Nasdaq        @ F
10:31:05.123  XYZ     100.05    300  Z  Cboe BZX      @ F
10:31:07.480  XYZ     100.04    200  D  FINRA TRF     @
```

The venue letter says where the trade happened. The condition codes describe the trade: `@` is a regular trade, and `F` marks an intermarket sweep order. A sweep is one order that is allowed to hit several venues at once instead of waiting for each better price to be routed in turn. A `D` print happened off-exchange, in a dark pool or at a wholesaler, and the tape does not say which one. FINRA publishes volume for each alternative trading system (ATS) only weekly, two to four weeks later. No print names the buyer or the seller, and none says which side was the aggressor. Researchers infer the side by comparing the trade price with the quote; the Lee-Ready rule does this.

**Options carry more labels, but still no names.** Electronic options trades are anonymous too. Nasdaq's options market says its trade reports "do not reveal contra party identities," and OCC stands between both sides at clearing. What options add is context. Here is a stylized slice of the options tape (OPRA):

```text
time          contract           price  size  exchange  condition
10:31:05.123  XYZ Nov-20 105 C    2.40   500  Cboe      SLAN  (filled in an auction)
10:31:06.004  XYZ Nov-20 105 C    2.45   200  ISE       ISOI  (part of a sweep)
```

Like the equity tape, it shows no buyer and no seller. The condition code adds context: it says whether the print came from an auction, a sweep, or a multi-leg (complex) order.

The richer clue comes before the trade. Options exchanges tag every order with an origin: priority customer, professional customer, broker-dealer, firm, or market maker. They need the tag because priority customers trade ahead of everyone else at the same price. Some of that tag reaches market data. Here is an example. A broker has a customer order to buy 500 calls and offers to fill it against its own account. Cboe first exposes the order in a short auction (AIM) so other firms can offer a better price. The auction notification it broadcasts looks like this:

```text
Cboe auction notification
symbol: XYZ 105 C   side: buy   contracts: 500   auction type: AIM
customer indicator: C (customer)     participant ID: (optional)
```

Market makers responding to that auction know the order is a customer's, and customer orders are less likely to be informed. The participant ID field can name the executing broker, but filling it in is optional. Other data products leak origin in aggregate. ISE's Top Quote feed shows customer size separately from professional size. Its Trade Outline product reports volume by origin type and by whether each trade opened or closed a position. Open interest, published the next day, shows whether yesterday's buyers opened new positions.

So the most an exchange shows is the type of trader, and sometimes the broker if that broker chooses to be named. No feed covered here shows the clearing firm or the end client. On a trading floor, the crowd sees which floor broker is representing the order, but not the broker's client.

**Can you work out who split a large order?** Usually you can tell that a stream of trades belongs to one order, but not whose order it is. In the equity tape example, three `F` prints in the same millisecond at the same price across three venues are almost certainly one buyer sweeping the offer. A parent order worked by an algorithm leaves a rhythm on the tape: 500 shares every 30 seconds, always lifting the offer. That tells you a patient buyer is likely still behind the market. It does not tell you the buyer is Fund X. This is Kyle's informed trader in practice. The trader breaks the order up so it looks like noise, and the market maker updates price as the one-sided flow accumulates. It is also why execution algorithms randomize child order sizes and timing.

**Where identity does leak.** Some flow arrives with a known source. The clearest case is a wholesaler, an off-exchange market maker such as Citadel Securities or Virtu that fills retail orders from its own inventory. When you buy 100 shares on Robinhood, the order usually goes to a wholesaler, not an exchange. The wholesaler sells to you slightly inside the exchange quote and often pays the broker for the order flow. It does not know who you are, but it knows the order came from Robinhood's retail customers, and that knowledge is what it is paying for. Retail orders are small and rarely carry information about where the price is going next, so the wholesaler can quote them tighter and still make money. The SEC calls this routing practice segmentation and notes that these orders "impose lower costs on liquidity providers than unsegmented order flow." A dealer asked for a risk price on a block also knows which client is asking. In both cases, knowing the source lowers adverse selection risk. That is why the same desk can quote a tight price to a retail broker's flow and a wide one to anonymous sweeps on the exchange.

```text
anonymous lit fill   -> know: price, size, venue, condition codes
options fill         -> also: auction / complex / origin context
segmented retail     -> also: which broker sent it
block risk request   -> also: which client is asking
```

## How Market Makers Protect Themselves

Market makers protect themselves in several ways.

They widen spreads when information risk rises. The wider spread makes each trade pay more for the chance of being wrong.

They reduce displayed size. A small stale quote is less dangerous than a large stale quote.

They update fast. If a related ETF, future, option, or peer moves, the quote changes before someone can trade against the old value.

They skew quotes. If buy flow looks informed, the ask moves up, the bid may move up too, and the market maker becomes less eager to sell.

They stop quoting or go manual in extreme cases. Around earnings, halts, macro data, or sudden news, the cost of being stale can exceed the spread.

Optiver's "pricing, risk, and execution" framing fits here: calculate theoretical value, measure the risk, then publish prices fast enough that the quote still reflects the risk. Adverse selection is what happens when that loop is too slow or the incoming flow knows something the model does not.

## Why Liquidity Can Disappear

Liquidity disappears when the cost of offering it becomes too high.

In an ordinary market, the next buyer might be a portfolio rebalance, a retail order, an ETF creation, or a trader with a mild view. In a news shock, the next buyer is more likely to be someone who saw the news faster, understood it better, or is trading against your stale price. The market maker cannot tell in advance, so the quote widens for everyone.

```text
news or uncertainty shock
  -> informed-flow probability rises
  -> stale quotes become dangerous
  -> market makers widen, shrink, or pull
  -> displayed liquidity falls when demand for liquidity rises
```

This is one reason stressed markets feel unfair. When you most want immediacy, the people who sell immediacy face the highest risk of being picked off.

## Common Misconceptions

Adverse selection is not the same as losing money after a trade. Prices can move against inventory for ordinary reasons. Adverse selection means the trade itself was more likely because the other side had better information.

All large flow is not toxic. A large index rebalance can be predictable and uninformed about fundamentals. It can still move price mechanically, but that is not the same as private information.

All informed trading is not illegal. A trader can build a better forecast from public data, speed, modeling, or research. The market maker still has to price the risk of trading with them.

Wider spreads are not only greed. They are often the market's way of charging for uncertainty about who is on the other side.

## Recap

Market makers lose money when they provide liquidity at stale prices to better-informed traders. This is adverse selection. A buy order can signal that the asset is worth more; a sell order can signal that it is worth less. Because the market maker cannot know which orders are informed, spreads widen when the probability or cost of informed trading rises. The desk habit is to ask: is this flow benign liquidity demand, mechanical demand, or a signal that fair value has changed?

## New Terms

**adverse selection**: The risk of trading with someone who has better information, so your quote is more likely to be wrong when it gets hit.

**informed flow**: Orders that are based on information or analysis that predicts future price moves.

**uninformed flow**: Orders driven by cash needs, indexing, hedging, rebalancing, or client demand, not by a superior view of value.

**consolidated tape (SIP)**: The public feed of every US trade and best quote. Each print shows price, size, time, venue, and condition codes, but never the buyer or seller.

**intermarket sweep order (ISO)**: An order allowed to trade at several venues at once instead of waiting to be routed to each better price in turn. It prints with condition `F` in equities and `ISOI` on OPRA.

**order origin**: The options label for who an order is for: priority customer, professional customer, broker-dealer, firm, or market maker. Exchanges use it for priority and fees.

**segmentation**: Routing a known type of flow, such as retail orders from one broker, to a liquidity provider who can price it separately from anonymous flow.

                                    ****

## Questions to Test Yourself

1. Why is selling to an informed buyer dangerous?

The buyer is more likely to trade when your ask is too low. You earn the spread, but then fair value moves above your sale price.

2. Why do spreads widen when uncertainty rises?

The next trader is more likely to know something or react faster than the market maker. The spread has to compensate for the larger expected loss to informed flow.

3. How do market makers protect themselves?

They widen spreads, reduce size, update quotes faster, skew away from risky flow, hedge, or stop quoting during extreme uncertainty.

4. Why can liquidity disappear when it is most needed?

The demand for immediacy rises at the same time the cost of providing immediacy rises. Market makers pull back because stale quotes can be picked off.

5. Three intermarket sweep (`F`) prints of XYZ at $100.05 hit NYSE Arca, Nasdaq, and Cboe BZX in the same millisecond. What can a market maker conclude about the buyer, and what can it not?

It is almost certainly one urgent buyer who paid to take every offer at once rather than wait, which makes the flow more likely to be informed and is a reason to raise the offer or cut size. The prints do not reveal who the buyer is, which clearing firm they use, or how much of the parent order is still left to buy.

## Sources

Glosten, Lawrence R., and Paul R. Milgrom. 1985. "Bid, Ask and Transaction Prices in a Specialist Market with Heterogeneously Informed Traders." *Journal of Financial Economics* 13 (1): 71-100. [https://doi.org/10.1016/0304-405x(85)90044-3](https://doi.org/10.1016/0304-405x(85)90044-3)

Kyle, Albert S. 1985. "Continuous Auctions and Insider Trading." *Econometrica* 53 (6): 1315-1335.

Easley, David, Robert F. Engle, Maureen O'Hara, and Liuren Wu. 2008. "Time-Varying Arrival Rates of Informed and Uninformed Trades." *Journal of Financial Econometrics* 6 (2): 171-207. [https://ideas.repec.org/a/oup/jfinec/v6y2008i2p171-207.html](https://ideas.repec.org/a/oup/jfinec/v6y2008i2p171-207.html)

Easley, David, Marcos Lopez de Prado, and Maureen O'Hara. "Flow Toxicity and Liquidity in a High-frequency World." [https://www.stern.nyu.edu/sites/default/files/assets/documents/con_035928.pdf](https://www.stern.nyu.edu/sites/default/files/assets/documents/con_035928.pdf)

Optiver. "Engineering the three pillars of trading: Pricing, risk, and execution." [https://www.optiver.com/insights/technology-blog/engineering-the-three-pillars-of-trading-pricing-risk-and-execution/](https://www.optiver.com/insights/technology-blog/engineering-the-three-pillars-of-trading-pricing-risk-and-execution/)
Lee, Charles M. C., and Mark J. Ready. 1991. "Inferring Trade Direction from Intraday Data." *Journal of Finance* 46 (2): 733-746.

Nasdaq. "Nasdaq TotalView-ITCH 5.0 Specification" (Add Order with MPID Attribution message). [https://nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/NQTVITCHspecification.pdf](https://nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/NQTVITCHspecification.pdf)

Nasdaq. SR-NASDAQ-2024-048, on trade reports that do not reveal contra party identities. [https://listingcenter.nasdaq.com/assets/rulebook/nasdaq/filings/SR-NASDAQ-2024-048_Notice_Approval.pdf](https://listingcenter.nasdaq.com/assets/rulebook/nasdaq/filings/SR-NASDAQ-2024-048_Notice_Approval.pdf)

Nasdaq ISE. SR-ISE-2026-17, on origin types reported in Trade Outline. [https://listingcenter.nasdaq.com/assets/rulebook/ise/filings/SR-ISE-2026-17.pdf](https://listingcenter.nasdaq.com/assets/rulebook/ise/filings/SR-ISE-2026-17.pdf)

SEC. 2011. Notice on the ISE Top Quote Feed, showing customer and professional size separately. [https://www.govinfo.gov/content/pkg/FR-2011-08-16/pdf/2011-20705.pdf](https://www.govinfo.gov/content/pkg/FR-2011-08-16/pdf/2011-20705.pdf)

SEC. 2022. "SEC Proposes Rule to Enhance Competition for Individual Investor Order Execution" (press release 2022-225). [https://www.sec.gov/news/press-release/2022-225](https://www.sec.gov/news/press-release/2022-225)

FINRA. Regulatory Notice 15-48, on ATS volume publication delays. [https://www.finra.org/rules-guidance/notices/15-48](https://www.finra.org/rules-guidance/notices/15-48)

Cboe. "Cboe Titanium U.S. Options Auction Feed Specification: Auction Notification Message Fields." [https://www.cboe.com/document/tech-spec/content/technical-specifications/cboe-titanium-u.s.-options-auction-feed-specification/cboe-options-auction-feed-messages/auction-notification-message-fields](https://www.cboe.com/document/tech-spec/content/technical-specifications/cboe-titanium-u.s.-options-auction-feed-specification/cboe-options-auction-feed-messages/auction-notification-message-fields)
