# Lesson 4: Price Formation, Information, and Mechanical Demand

## Learning Goal

Lesson 3 explained why large or urgent trades move prices. This lesson asks a sharper question: *why* did the price move?

"XYZ is up 3%" is not an explanation. Either the market revised its estimate of value, or someone needed liquidity, or both. A flows desk has to separate those mechanisms. The same print can be information, mechanical demand, or a mix, and the mix decides whether the move is likely to stick or fade.

## The Problem: Two Ways a Price Can Change

XYZ last traded at $100. An hour later it trades at $103. What happened?

One possibility: new information arrived. Earnings beat, a drug worked, a competitor failed. Investors revised expected cash flows or risk. The new price is a new estimate of value.

The other possibility: someone needed to buy or sell a lot of stock, and there were not enough willing counterparties at $100. The price had to move to clear the trade. No one learned a new fact about the business. The market learned that there was a large liquidity demand.

```text
price moved
  |
  +--> beliefs about value changed     -> information / price discovery
  |
  +--> required trade met scarce liquidity -> mechanical / liquidity demand
```

Both can be true at once. A merger is news *and* it can force index funds, arb desks, and hedgers to trade.

## A Small Worked Example

Three stories, same tape: XYZ $100 to $103 on heavy volume.

**Case A — information.** XYZ reports earnings that beat by $0.40. Analysts raise next year's earnings. Buyers who think $100 is now too cheap lift offers. Liquidity providers update: the stock is probably worth more. $103 can be the new consensus even after the burst of trading ends.

**Case B — mechanical demand.** S&P announces XYZ will enter the S&P 500 after Friday's close. Index funds must own it by the implementation print. Nothing changed about XYZ's products. Funds still have to buy a known number of shares by a known deadline. Offers get lifted because the buyers cannot walk away.

**Case C — both.** XYZ agrees to be acquired. The cash-flow story changed, *and* index and arb desks must reposition. You cannot read "up 3%" and pick one slogan.

The desk question is never only "did it go up?" It is "which channel, how much flow is left, and should this persist?"

## How Information Gets Into Prices

Price discovery is the process of turning scattered beliefs into a traded price. Informed traders buy when they think the stock is cheap relative to their estimate of value. Their orders consume liquidity. Other traders update: someone is lifting the offer; maybe they know something. Quotes adjust.

That is the Glosten-Milgrom (1985) idea: the spread compensates a liquidity provider for the risk of trading against someone better informed. A buy is more likely to come from a trader who thinks the asset is worth more, so the ask sits above the bid. Kyle (1985) makes the same point in an auction: an insider hides in uninformed "noise" order flow, and the market maker sets a price that is a linear function of net order flow. In both models, trades are signals. Hasbrouck later put it bluntly: it can be more accurate to say that orders *forecast* prices than that they mechanically shove them.

Jane Street's Signals and Threads conversation on machine learning in markets draws the same line in desk language. Sometimes the person trading with you knows something you do not. Sometimes they are doing a large transaction as ordinary business, and it does not reflect private information about the company. Knowing which one you are facing changes the price you are willing to show, because the information content of the order is different.

A common mistake is to treat every aggressive buy as "smart money." Uninformed size looks the same on an anonymous tape. Bouchaud and others emphasize the implication: if the market cannot see who is informed, then random liquidity demand also moves prices. Impact is how information gets in, *and* how noise gets in.

Lesson 6 goes deeper on adverse selection. Here the point is only that prices update from order flow because that flow might contain information.

## Mechanical Demand and Downward-Sloping Demand

Mechanical demand is required buying or selling created by a rule, benchmark, hedge, or cash need, not by a new view on the company's value. Index adds and deletes are the clean teaching case, because the methodology is public and the funds cannot skip the name.

If stocks were perfect substitutes, extra buying by index funds would not raise the added stock's price. Arbitrageurs would sell the add and buy a twin, and the demand curve would stay flat. Shleifer (1986) used S&P 500 inclusions after 1976 as a test. Newly added stocks earned a significant positive abnormal return at announcement, about 2.8% in his 1976–1983 sample. The return did not vanish for at least ten days. It lined up with measures of index-fund buying, and not with S&P bond ratings, which is a strike against a simple "inclusion certifies quality" story. His conclusion: demand curves for stocks slope down. You have to pay more to buy more, because other holdings are imperfect substitutes and arbitrage is risky.

Harris and Gurel (1986) used the same laboratory and stressed the other reading. S&P list changes make investors rebalance, and they are unlikely to reveal much about the firm's future products. They found prices rose more than 3% right after an addition was announced, and that rise was nearly fully reversed after two weeks. That is the price-pressure hypothesis: temporary liquidity demand, then fade.

Those two 1986 papers are the argument you still hear on a desk. Shleifer: lasting extra demand, imperfect substitutes. Harris-Gurel: temporary pressure that should come back once the forced buying is done.

Later work did not pick one slogan. Kaul, Mehrotra, and Morck (2000) studied a Toronto Stock Exchange 300 float-definition change that altered weights, conveyed no firm news, and produced about 2.3% excess return in the event week with no reversal as volume normalized. That is closer to a pure demand-curve shift. Petajisto (2011) measured announcement-to-effective-day moves from 1990 to 2005 of about +8.8% for S&P 500 adds and +4.7% for Russell 2000 adds, with large opposite moves for deletions. Most of that effect was still there two weeks later. He treated the premium as a hidden cost that index funds pay because they must trade into a known demand shock.

The size of the *average* S&P add return is not a constant. Greenwood and Sammon (2025) document that the inclusion effect grew into the 1990s and then fell toward something statistically indistinguishable from zero in the 2010s, even as passive assets grew. Their main explanations are mechanical offset (more adds are migrations from the S&P MidCap 400, so MidCap trackers are forced sellers while S&P 500 trackers are forced buyers) and a much smaller price impact per unit of demand as other institutions learned to absorb the shock. The mechanism did not disappear. The easy, uncrowded version of the trade did.

```text
index add announced
  -> estimate forced buy shares
  -> compare to ADV and auction size
  -> anticipatory trading can lift the price early
  -> trackers finish near the close
  -> some of the move may fade; some may stick as extra indexer demand
```

## Feedback Between Prices and Positioning

Prices and positions feed each other.

A rising price can force more mechanical buying: a stock that grows into an index, a momentum sleeve that must add, a CTA that flips long, a levered ETF that rebalances with the move. A falling price can force selling: margin, risk limits, target-volatility funds, deletions. The second wave is not new information about the company. It is a rule hitting a new price.

The other direction: positioning changes what the next order means. If everyone who had to buy is already long, the remaining tape is more likely information or discretionary flow. If a large forced buyer is still unfinished and the deadline is public, the next lift of the offer is more likely leftover mechanical demand.

```text
price change
  -> rules and limits trigger more trades
  -> those trades move price again
  -> later orders are read against that positioning
```

That loop is why "the stock is up, so someone knows something" is a weak default. Sometimes the stock is up because yesterday's price tripped a mandate.

## How a Desk Tries to Tell the Channels Apart

You cannot see beliefs. You infer the mix.

Look for a public information event: earnings, guidance, a drug result, a merger filing. If related names and the sector move the same way, information is more plausible. If only the name with a known forced trade moved, mechanical demand is more plausible.

Look at the calendar. An index announcement, a reconstitution close, a month-end rebalance, or an option expiry is a reason to expect liquidity demand on a clock. Lesson 3's point still applies: predictable buyers can pay before they finish.

Look at size versus liquidity. A 50,000-share print in a name that trades 20 million shares a day is a weak mechanical story. A buy that is a large slice of ADV into Friday's close, with published tracker AUM, is a strong one.

Look at what happens after the forced flow ends. Fade after the deadline is evidence of temporary pressure. No fade is not automatic proof of information. Persistent extra demand from indexers can hold a premium even if no cash-flow news arrived. That is the Shleifer / Harris-Gurel split, still live after Petajisto and after the later shrinkage of the average add return.

Volume alone does not decide. Both a surprise earnings print and a reconstitution close produce volume.

## Common Misconceptions

Every uptick is not "the market learned something." A lot of price change is inventory and flow.

Mechanical flow is not "fake." It is real demand. It just is not a research view on the company's products.

If the price does not fully reverse after an index event, that does not prove the add was information. Persistent extra demand from indexers can hold a premium. Harris-Gurel and Shleifer were arguing about that split, and later samples still do not give one permanent percentage.

The index effect is not a reliable 3% coupon. The 1980s and 1990s averages were large. Recent S&P 500 addition returns have been much smaller on average, in part because the other side learned the trade and because MidCap migrations offset some of the shock. The desk still estimates the flow. It does not assume last decade's premium.

## Recap

Prices form when orders meet liquidity. Sometimes the order exists because someone updated their estimate of value. Sometimes it exists because a rule, hedge, or cash need requires a trade. Mechanical demand can move prices without new fundamental news because stock demand curves are not perfectly flat, especially in the short run. Information and flow often arrive together. Later prices can trigger more mechanical trading, and leftover positioning changes how the next print should be read. The desk question is never only "did it go up?" It is "what mechanism, how much is left, and should this persist?"

## New Terms

**price discovery**: The process of turning orders and information into a traded price that reflects current beliefs about value.

**informed trading**: Trading based on a view that the current price is wrong relative to estimated value.

**uninformed / liquidity trading**: Trading to raise cash, hedge, rebalance, or meet a mandate, not to express a new valuation view.

**mechanical demand**: Required buying or selling created by a rule or benchmark, such as an index add.

**price pressure**: A price move caused by temporary liquidity demand that is expected to fade after the trade is done.

**downward-sloping demand**: The idea that you must pay a higher price to buy more of a stock because other holdings are imperfect substitutes.

**index premium**: Extra price associated with index membership, paid in part because passive capital must own the name.

## Questions to Test Yourself

1. Did price move because the market learned something?

Only if beliefs about cash flows or risk changed. A print can also be a liquidity or mechanical demand shock with no new business news.

2. Did price move because someone needed liquidity?

Yes when size, urgency, or a rule forced a trade and counterparties required a better price to take the other side. That is price pressure or downward-sloping demand, not a new earnings estimate.

3. Can information and mechanical pressure both matter?

Yes. A merger or an index add can change the story and force trading at the same time. Separate the channels instead of picking one slogan.

4. How would you distinguish a fundamental repricing from temporary flow pressure?

Look for news and related-name moves versus a known forced-trade deadline, size versus liquidity, and whether the move fades after the flow ends. Persistence can still be extra indexer demand, not proof of information.

## Sources

Shleifer, Andrei. 1986. "Do Demand Curves for Stocks Slope Down?" *Journal of Finance* 41 (4): 579–590. https://doi.org/10.1111/j.1540-6261.1986.tb04518.x

Harris, Lawrence, and Eitan Gurel. 1986. "Price and Volume Effects Associated with Changes in the S&P 500 List: New Evidence for the Existence of Price Pressures." *Journal of Finance* 41 (4): 815–829. https://doi.org/10.1111/j.1540-6261.1986.tb04550.x

Glosten, Lawrence R., and Paul R. Milgrom. 1985. "Bid, Ask and Transaction Prices in a Specialist Market with Heterogeneously Informed Traders." *Journal of Financial Economics* 13 (1): 71–100. https://doi.org/10.1016/0304-405x(85)90044-3

Kyle, Albert S. 1985. "Continuous Auctions and Insider Trading." *Econometrica* 53 (6): 1315–1335.

Kaul, Aditya, Vikas Mehrotra, and Randall Morck. 2000. "Demand Curves for Stocks Do Slope Down: New Evidence from an Index Weights Adjustment." *Journal of Finance* 55 (2): 893–912. https://doi.org/10.1111/0022-1082.00230

Petajisto, Antti. 2011. "The Index Premium and Its Hidden Cost for Index Funds." *Journal of Empirical Finance* 18 (2): 271–288. https://petajisto.net/papers/petajisto%202011%20jef%20-%20hidden%20cost%20for%20index%20funds.pdf

Greenwood, Robin, and Marco Sammon. 2025. "The Disappearing Index Effect." *Journal of Finance*. Working version: https://www.ivey.uwo.ca/media/m2kh5j5y/the-disappearing-index-effect.pdf

Jane Street. "Finding Signal in the Noise: Machine Learning and the Markets." *Signals and Threads*. https://signalsandthreads.com/finding-signal-in-the-noise/
