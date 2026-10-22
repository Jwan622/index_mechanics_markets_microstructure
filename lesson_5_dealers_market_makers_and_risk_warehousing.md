# Lesson 5: Dealers, Market Makers, and Risk Warehousing

## Learning Goal

Lesson 4 asked why a price moved: information, mechanical demand, or both. This lesson asks who takes the other side when someone needs to trade now.

Often there is no natural buyer waiting at the old price. A dealer or market maker buys what the client sells, holds the risk for a while, and tries to get out later. That temporary holding is risk warehousing. Liquidity is often someone else accepting risk on their own balance sheet.

## The Problem: The Client Wants Out Now

A pension fund must sell 200,000 shares of XYZ by the close. Mid is $100. The displayed bid shows a few thousand shares. There is no other fund that wants those 200,000 shares at $100 this minute.

Two paths.

The broker can work the order as agent: look for other buyers, slice the order, ping dark pools, work the close. The firm does not own the shares. It charges a commission. The fund still owns the risk until a buyer is found.

Or the dealer can buy the block as principal. The fund is done. The dealer now owns 200,000 shares. If XYZ falls, the dealer loses. That is facilitation: the firm uses its own capital so the client can finish.

FINRA puts the same split in regulatory language. A principal trade is a trade for an account the broker-dealer owns. The firm usually charges a markup, markdown, or commission-equivalent. An agency trade is an intermediary trade for the customer with a third party. It does not pass through the firm's proprietary book. The firm usually charges a commission.

```text
client needs to sell
  |
  +--> agency: broker finds a buyer; client keeps the risk until filled
  |
  +--> principal: dealer buys the stock; dealer now has the risk
```

Lesson 2's DCP and RFQ path is principal. The streamed or requested quote is the dealer offering to warehouse size.

## A Small Worked Example

XYZ mid is $100. A market maker's theoretical value is also $100. Optiver's explainer is the clean picture: compute a theoretical price, then add a margin for the risk of quoting. They show $99.95 bid / $100.05 ask for 1,000 shares. If one person sells and one person buys, the firm keeps ten cents if nothing else moves.

Now the pension fund wants 200,000 shares done. The dealer bids $99.90 for the block. The fund sells. The fund's problem is over. The dealer's problem has started.

```text
before:  dealer flat, quotes around $100
trade:   dealer buys 200,000 at $99.90
after:   dealer long 200,000 shares
```

If XYZ is still $100 an hour later and the dealer sells at $99.98, the warehouse made eight cents a share. If XYZ gaps to $99.00 on the next print, the position is underwater by $0.90 a share, or $180,000, before hedges. The client paid a concession for certainty. The dealer got paid to take a risk that can be larger than that concession.

## Why Inventory Is Risk

Inventory is the position the dealer is holding because it traded. Long inventory means the firm bought more than it sold. Short inventory means the opposite.

The risk is simple: the price can move before the firm gets out. Time makes it worse. Volatility makes it worse. Size makes it worse. A name that does not hedge cleanly makes it worse.

Ho and Stoll (1981) modeled the dealer as someone who must quote while facing two uncertainties: the stock's return, and when the next offsetting trade will arrive. The longer the wait, the longer the firm bears return risk. The bid and ask they set depend on that risk, on trade size, and on how much inventory they already have. They lower both quotes when they are long, to attract buyers and discourage more sellers.

The firm's balance sheet is the limit on how much of this it can do. Capital, haircuts, internal risk limits, and overnight constraints cap the warehouse. A desk that is already long index futures, long a sector, and long three related names has less room for the next 200,000-share XYZ bid, even if the "fair" value has not changed.

## How the Dealer Hedges

The dealer does not have to keep the raw 200,000-share bet. It can transfer part of the risk to another instrument.

If XYZ is a large S&P name, selling S&P futures or an S&P 500 ETF hedges the market piece. If the worry is the industry, a sector ETF or a basket of peers hedges more of the residual. The leftover after a hedge is basis risk: XYZ can still fall while the hedge rises.

```text
buy 200,000 XYZ from the fund
  -> sell futures / ETF / peers
  -> market risk down, XYZ-specific risk still there
  -> later, sell XYZ and buy back the hedge
```

Hedging is also a flow. The dealer's futures sale is someone else's print. A large facilitation can show up as pressure in the stock *and* in the hedge. That is why a flows desk watches related markets after a known block, not only the name.

Optiver describes the same loop as three pillars: price the instrument, measure the risk and the margin that risk requires, then execute fast enough that the quote still matches the risk. If risk updates and the quote does not, the firm is offering yesterday's warehouse at today's price.

## Why the Warehouse Has a Cost

The client pays because the dealer is using scarce things: capital, risk limits, and attention.

A wider spread or a larger concession is the posted price of that service. Higher volatility raises the chance the inventory moves against the firm before it exits, so quotes widen or size shrinks. A longer expected hold — a dull name, a one-sided day, a position that is hard to hedge — costs more. Overnight and weekend gaps cost more than an intraday flip.

Competition works the other way. Optiver's explainer says more market makers in the same name usually means tighter spreads, because each firm is bidding to be the warehouse. The spread is not a fee for "being in the market." It is compensation for standing there with a book that can lose money.

Avellaneda and Stoikov (2008) write the lean in one line of logic. If you are already long, your reservation price — the price at which you are willing to hold more — sits below the mid. You bid less eagerly and offer more eagerly, so inventory is pushed back toward flat. That is quote adjustment, not a new view on the company's products.

## Why Appetite Changes in Stress

Appetite is how much inventory the firm will take at a given concession.

In calm markets, hedges are cheap, limits have room, and the next offsetting flow is likely. The dealer can bid for 200,000 shares. In stress, volatility jumps, correlations break, futures get expensive or jumpy, and every desk is already long the same risk. The same 200,000 shares now consume more of the limit. Quotes widen, sizes drop, or the firm only offers agency.

The firm did not "run out of liquidity" as an abstract substance. It ran out of willingness to warehouse, given the risk per share and the room left on the book. Lesson 6 covers a second reason quotes disappear: the other side may know something. Here the point is inventory and capacity.

## Common Misconceptions

The dealer is not the natural other side in the economic sense. It is a temporary other side. It still has to find a home for the risk.

A tight printed spread does not mean the dealer will take your block. Displayed size is a small quote. Facilitation is a separate decision about inventory.

Hedging does not make the trade free. It swaps one risk for a smaller, different risk, and the hedge itself can move prices.

If the stock falls after the dealer bought the fund's shares, that is not proof the fund "knew." It is what inventory risk looks like. Whether the flow was informed is a later question.

## Recap

When a client needs to trade now, someone must take the risk. An agency broker searches for a match and leaves the risk with the client until a fill. A principal dealer buys or sells for its own account and warehouses the position. Inventory is risky because price can move before the firm exits. The firm charges a spread or concession, leans its quotes to shed the position, and often hedges in futures, ETFs, or related names. Appetite shrinks when volatility, limits, or broken hedges make each extra share more expensive to hold. Liquidity, in this lesson, is that willingness to hold risk for a while.

## New Terms

**dealer / market maker**: A firm that quotes or trades as principal and takes the other side using its own capital.

**principal trade**: A trade for the broker-dealer's own account. The firm takes inventory risk.

**agency trade**: A trade the firm works for the customer with a third party, without putting the shares on its own book.

**facilitation**: Principal trading done to complete a client's order, usually a block, by warehousing the risk.

**inventory**: The position a dealer holds because it has traded more one way than the other.

**risk warehousing**: Holding that inventory for a period so the client can be done now.

**quote adjustment / leaning**: Moving the bid and ask to attract offsetting flow and discourage more of the same side.

**reservation price**: The dealer's inventory-adjusted value; below the mid when long, above the mid when short.

**basis risk**: The risk left after a hedge, because the hedge and the position do not move one-for-one.

## Questions to Test Yourself

1. What happens when a dealer buys what a client sells?

The client is flat. The dealer owns the shares and the price risk until it sells or hedges them away.

1. Why does inventory create risk?

The price can move before the dealer gets out. Larger size, more time, and higher volatility make that loss bigger.

1. How might a dealer hedge that risk?

Sell or buy a related instrument — futures, an ETF, or peers — so market or sector moves hurt less. XYZ can still move against the leftover basis.

1. Why does risk warehousing have a cost, and why might appetite fall in stress?

The dealer uses capital and limits to hold a position that can lose money, so it charges a spread or concession. In stress those limits fill up, hedges get worse, and the firm takes less size at any given price.

## Sources

Optiver. "Market Making." [https://www.optiver.com/insights/explainers/market-making/](https://www.optiver.com/insights/explainers/market-making/)

Optiver. "Engineering the three pillars of trading: Pricing, risk, and execution." July 4, 2024. [https://www.optiver.com/insights/technology-blog/engineering-the-three-pillars-of-trading-pricing-risk-and-execution/](https://www.optiver.com/insights/technology-blog/engineering-the-three-pillars-of-trading-pricing-risk-and-execution/)

FINRA. "Compensation and Mixed Capacity Trading." [https://www.finra.org/sites/default/files/NoticeDocument/p003505.pdf](https://www.finra.org/sites/default/files/NoticeDocument/p003505.pdf)

Ho, Thomas, and Hans R. Stoll. 1981. "Optimal Dealer Pricing under Transactions and Return Uncertainty." *Journal of Financial Economics* 9 (1): 47–73. [https://doi.org/10.1016/0304-405x(81)90020-9](https://doi.org/10.1016/0304-405x(81)90020-9)

Avellaneda, Marco, and Sasha Stoikov. 2008. "High-frequency Trading in a Limit Order Book." *Quantitative Finance* 8 (3): 217–224.