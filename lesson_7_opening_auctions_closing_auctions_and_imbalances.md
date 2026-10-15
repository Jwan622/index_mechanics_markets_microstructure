# Lesson 7: Opening Auctions, Closing Auctions, and Imbalances

## Learning Goal

Lessons 2 through 6 described continuous trading: orders arrive one at a time, hit the book, and trade immediately at whatever is resting there. This lesson covers the other way exchanges match orders: collect them for a while, then trade them all at once at a single price.

That is an auction. U.S. stocks open and close with one every day, and the closing auction is where a large share of index-related trading happens. The goal is to understand why benchmarked money concentrates at the close, how the exchange picks the closing price, what the imbalance messages before the close are telling you, and what goes wrong when too much one-sided flow arrives at once.

## The Problem: Many Traders Want the Same Price

An S&P 500 index fund holds XYZ. Tonight the index level is computed from XYZ's official closing price, and the fund's net asset value (NAV) is struck from the same price. The fund is judged on how closely its NAV follows the index.

Suppose the fund must buy 10,000 shares of XYZ today because of a rebalance. It could buy at 2:00 p.m. for $49.90, or in the closing auction at whatever the close turns out to be.

If the close is $50.02, the 2:00 p.m. purchase beat the index by 12 cents a share. That sounds good, but it is luck in both directions: if the close had been $49.80, the same purchase would have lagged the index by 10 cents. The fund is not paid to bet on intraday moves. It is paid to match the index. Buying at the closing price, which is the price the index itself uses, removes that gap. The difference between fund and index return is called tracking error, and trading at the close is the simplest way to keep it near zero.

Every passive fund tracking an index that uses closing prices has the same incentive. So do benchmarked active managers whose performance is measured from close to close, and funds that must value holdings at the close. A continuous market cannot give thousands of participants *the same* price: each fill happens at its own moment and price. An auction can.

## How an Auction Works

In an auction, the exchange stops matching orders immediately. It collects orders in a separate book until a set time, then finds one price at which as many shares as possible can trade, and executes every matched order at that one price. This is called a call auction or a single-price (uniform-price) auction.

The orders specific to the close:

- A **market-on-close (MOC)** order says "buy (or sell) this many shares at whatever the closing price is." It is guaranteed to participate if there is anyone on the other side, but it gives up all control over price.
- A **limit-on-close (LOC)** order says "buy at the closing price, but only if that price is at or below my limit" (or at or above, for a sell). It controls price but may not fill.
- **Imbalance-only liquidity**: Nasdaq's Imbalance-Only (IO) orders and NYSE's Closing Offset (CO) orders only trade against the side that has excess interest. They exist to let liquidity providers offset an imbalance without adding to it.

On both NYSE and Nasdaq, MOC and LOC orders must be entered by 3:50 p.m. Eastern. After that, NYSE only accepts orders on the side that offsets the published imbalance, and limits cancellations to documented errors. The auction runs at 4:00 p.m. These cutoffs have changed over the years and differ in detail between exchanges, so the current rulebook, not a lesson, is the source of truth.

## A Small Worked Example: Finding the Closing Price

XYZ's continuous market is $49.98 bid / $50.02 ask, so the mid is $50.00. At 3:50 p.m. the closing book holds:

```text
buy  MOC              30,000
buy  LOC  $50.05      10,000
buy  LOC  $49.95      20,000

sell MOC              15,000
sell LOC  $49.98      10,000
sell LOC  $50.10      20,000
```

For any candidate closing price, a buy order participates if its limit is at or above that price (MOC always participates). A sell participates if its limit is at or below that price. The shares that can actually trade are the smaller of the two totals. Checking each limit price:

```text
price    buyers willing   sellers willing   matched   imbalance
49.95        60,000           15,000         15,000    45,000 buy
49.98        40,000           25,000         25,000    15,000 buy
50.05        40,000           25,000         25,000    15,000 buy
50.10        30,000           45,000         30,000    15,000 sell
```

The exchange picks the price that maximizes matched shares: **$50.10, with 30,000 shares**. Every matched trade happens at $50.10. The MOC buyer pays ten cents above the mid. The LOC buyer at $50.05 does not fill at all. The sellers fill in price priority: the 15,000 MOC shares and the 10,000 shares at $49.98 fill completely, and the seller at $50.10 fills only 5,000 of 20,000.

This is the imbalance problem in one picture. There were 30,000 shares of buy MOC, which must trade at any price, but only 25,000 shares of sell interest below $50.10. The price had to climb to the next seller.

## The Imbalance Message Attracts the Other Side

Starting at 3:50 p.m., both exchanges publish imbalance information about the closing book. For the book above, at a reference price of $50.00 the message says, in effect:

```text
paired shares:     25,000
imbalance:         15,000 to BUY
indicative price:  50.10
```

(The exact fields differ by exchange. NYSE publishes paired and unpaired quantity, a closing-only interest price, and a continuous-book clearing price, updating every second when something changes. Nasdaq's Net Order Imbalance Indicator includes paired shares, imbalance size and side, a "near" price that combines the closing book with the continuous book, and a "far" price from the closing book alone.)

To a liquidity provider, this message is an invitation. Someone must buy 15,000 more shares at the close, and the indicative price is ten cents above the mid. A market maker who can sell 15,000 shares at about $50.02 and buy them back after the close or tomorrow morning will usually make money, for reasons Lessons 5 and 6 explain: the buyer is visibly mechanical, so the information risk is low, and the price concession is visible in advance.

Suppose a liquidity provider adds `sell LOC $50.02  15,000`. Recompute:

```text
price    buyers willing   sellers willing   matched   imbalance
49.95        60,000           15,000         15,000    45,000 buy
49.98        40,000           25,000         25,000    15,000 buy
50.02        40,000           40,000         40,000         0
50.05        40,000           40,000         40,000         0
50.10        30,000           60,000         30,000    30,000 sell
```

Now two prices tie at 40,000 matched shares with zero imbalance. Nasdaq's tie-break, after maximizing matched shares and minimizing imbalance, is the price closest to the inside midpoint. That picks **$50.02**. The closing price dropped eight cents, matched volume rose from 30,000 to 40,000, and the LOC buyer at $50.05 now fills.

It helps to put dollars on who won and who lost. Assume XYZ opens tomorrow at the old mid of $50.00, because nothing was learned about the company:

```text
                                   without offset     with offset
closing price                         $50.10            $50.02
MOC buyer's premium over the mid      $0.10 x 30,000    $0.02 x 30,000
                                      = $3,000          = $600
liquidity provider                    not involved      sold 15,000 at $50.02,
                                                        buys back at $50.00
                                                        = +$300
```

The liquidity provider's $300 is not free money. It carried a 15,000-share short overnight, and if XYZ opened at $50.50 on news, it would have lost $7,200. That is Lesson 5's inventory risk, now with an overnight gap in it. The provider is willing to take that risk because the imbalance is public and mechanical, which is Lesson 6's low-μ case. The MOC buyer is better off too: it saved $2,400, even though someone else made $300 from its order.

The general mechanism:

```text
mechanical MOC flow enters by 3:50
   |
   v
exchange publishes imbalance and indicative price
   |
   v
liquidity providers see a visible, mostly uninformed imbalance
   |
   v
they add offsetting orders (LOC, IO, CO)
   |
   v
imbalance shrinks, closing price moves back toward fair value
   |
   v
providers carry the inventory overnight or unwind it next morning
```

## Why the Maximum-Volume Price Is Where Supply Meets Demand

The rule "maximize matched shares" is not arbitrary. It finds the price where the auction's own demand and supply curves cross.

As the candidate price rises, the number of shares buyers are willing to buy can only fall or stay the same, because each LOC buyer drops out once the price passes their limit. The number of shares sellers are willing to sell can only rise or stay the same. Matched volume is the smaller of the two.

Below the crossing point, sellers are the smaller side. Raising the price adds sellers, so matched volume rises. Above the crossing point, buyers are the smaller side. Raising the price removes buyers, so matched volume falls. Matched volume therefore peaks at the crossing, which is the price where buy and sell quantities are as close to equal as the orders allow. Because orders come in lumps, the curves can cross in a range rather than at a single point, which is why the exchange needs the second and third rules (minimize imbalance, then stay near the mid) to pick one price.

A short Python version of the rule:

```python
def closing_auction_price(closing_orders, reference_mid):
    """Return the price that maximizes matched shares, then minimizes imbalance, then is closest to the mid."""
    limit_prices = {order["limit"] for order in closing_orders if order["limit"] is not None}
    candidate_prices = sorted(limit_prices | {reference_mid})  # the mid matters if the book is all MOC
    best_ranking_key, best_price, best_matched_shares = None, None, None
    for price in candidate_prices:
        buy_shares_willing = sum(
            order["shares"] for order in closing_orders
            if order["side"] == "buy" and (order["limit"] is None or order["limit"] >= price)
        )
        sell_shares_willing = sum(
            order["shares"] for order in closing_orders
            if order["side"] == "sell" and (order["limit"] is None or order["limit"] <= price)
        )
        matched_shares = min(buy_shares_willing, sell_shares_willing)
        imbalance_shares = abs(buy_shares_willing - sell_shares_willing)
        ranking_key = (-matched_shares, imbalance_shares, abs(price - reference_mid))
        if best_ranking_key is None or ranking_key < best_ranking_key:
            best_ranking_key, best_price, best_matched_shares = ranking_key, price, matched_shares
    return best_price, best_matched_shares


closing_book = [
    {"side": "buy", "limit": None, "shares": 30_000},   # MOC: limit None
    {"side": "buy", "limit": 50.05, "shares": 10_000},
    {"side": "buy", "limit": 49.95, "shares": 20_000},
    {"side": "sell", "limit": None, "shares": 15_000},
    {"side": "sell", "limit": 49.98, "shares": 10_000},
    {"side": "sell", "limit": 50.10, "shares": 20_000},
]
closing_auction_price(closing_book, reference_mid=50.00)   # (50.10, 30000)

closing_book.append({"side": "sell", "limit": 50.02, "shares": 15_000})
closing_auction_price(closing_book, reference_mid=50.00)   # (50.02, 40000)
```

This is a simplification. Real auctions also include the continuous book (on Nasdaq, resting orders in the regular book join the cross), apply price bands, and handle imbalance-only orders specially. The core ranking, though, is the one Nasdaq publishes.

## Reading an Imbalance Like a Desk

An imbalance number on its own means little. "15,000 to buy" is huge in a stock that trades 50,000 shares at the close and is nothing in one that trades 5 million. A desk usually reads it in three steps. This is a working heuristic, not an exchange rule.

First, scale it. Divide the imbalance by the stock's typical closing auction volume, and by its average daily volume (ADV). Lesson 3's point was that size only means something relative to available liquidity.

```text
stock    imbalance    typical close volume    imbalance / close volume
XYZ       15,000            200,000                  7.5%
ABC      300,000            200,000                  150%
```

XYZ's imbalance will probably be absorbed by ordinary offsetting liquidity. ABC's imbalance is larger than a normal day's whole closing auction, so the price will probably have to move to attract enough sellers.

Second, watch how it changes. Between 3:50 and 4:00, the imbalance either shrinks as offsetting orders arrive or stays large because nobody wants the other side. A shrinking imbalance with the indicative price moving back toward the mid is the offset mechanism working. An imbalance that stays large with the indicative price drifting away from the mid is the warning sign.

Third, ask why it exists. A large imbalance on an index rebalance day, matching the flow you estimated in advance, is mechanical and mostly uninformed. A large imbalance on an ordinary day after late news might not be. The same number calls for a different price depending on that answer, which is the whole of Lesson 6 applied to the close.

## The Opening Auction

The opening auction solves a different problem. Overnight, news arrives, foreign markets trade, and futures move, but the stock has not traded. At 9:30 a.m., the first price needs to absorb all of that at once. If the market simply opened continuous trading, the first few orders would trade against whatever stale limit orders happened to be sitting in the book, and those resting orders would be picked off, which is Lesson 6's free-option problem at its worst.

An opening auction collects overnight orders, publishes imbalance information before the open, and finds one price for all of them. It pools the overnight information into a single price rather than letting a few fast orders pick it off. Index flow concentrates far less at the open than at the close, because index levels and fund NAVs are calculated from closing prices, but some event-driven flow, such as trades that must follow an overnight announcement, does use the open.

## Why Flow Concentrates at the Close

The close has become one of the most important liquidity events of the day. Bogousslavsky and Muravyev found the U.S. closing auction accounted for 7.5% of daily volume in 2018, up from 3.1% in 2010, and attribute part of the shift to the growth of indexing and ETFs. On index event days the concentration is far larger. Nasdaq reported that its closing cross on the 2026 Russell reconstitution day executed 4.59 billion shares, worth about $334 billion, in 1.63 seconds.

The reasons reinforce each other:

1. **Benchmark matching.** Index levels and fund NAVs use closing prices, so trading at the close minimizes tracking error.
2. **Liquidity attracts liquidity.** Because many natural buyers and sellers show up at the close, it is a good place to find the other side, so more traders come.
3. **Visible, uninformed imbalance.** Liquidity providers can see the imbalance and know most of it is mechanical. That lowers the information charge from Lesson 6.
4. **Single price, no queue race.** Everyone in the match gets the same price, so a slow trader is not picked off by a fast one within the auction.

## What Can Go Wrong When Too Much Flow Concentrates

The close works when the offsetting liquidity that arrives after 3:50 is large enough relative to the imbalance. When it is not, the price has to move until enough sellers (or buyers) appear, exactly as the first worked example moved from $50.00 to $50.10.

Bogousslavsky and Muravyev found that closing prices often deviate from the closing quote midpoint, and that these deviations revert by about half shortly after the close and fully overnight. That reversal is the signature of temporary price pressure from Lesson 4: the close moved because liquidity was demanded, not because anything was learned. They also found the closing auction contributes little to price discovery relative to its volume.

Exchanges limit how far the close can move. Nasdaq's FAQ describes a threshold for the closing cross of the greater of $0.50 or 10% from the midpoint, with tighter bands for exchange-traded products. These bands stop a catastrophic print but do not prevent a price that is meaningfully distorted within the band.

A subtle consequence: the index fund that buys at a distorted close shows zero tracking error, because the index uses the same distorted price. The cost is still real. The fund bought at $50.10 a stock that trades at $50.00 the next morning, and so did the index. Fund investors pay that cost, but it is invisible in the tracking-error report. This is closely related to Petajisto's "hidden cost" from Lesson 4.

Predictability makes this worse as well as better. If everyone can estimate an index fund's closing buy days in advance, some traders buy earlier and plan to sell into the close. That can supply liquidity at the auction, but it can also raise the price the fund pays before the close even starts. Lesson 16 returns to this crowding problem.

## Common Misconceptions

A common mistake is to think the closing price is just the last trade of continuous trading. For U.S. listed stocks, it is the result of a separate auction with its own order book, its own order types, and its own price-setting rule.

Another is to read an imbalance message as a forecast of direction. A large buy imbalance at 3:50 does not mean the close will be up. It is an invitation for offsetting liquidity, and if enough arrives, the imbalance can shrink to zero and the price can settle near the mid.

It is tempting to think MOC orders are "free" because they get the benchmark price. They give up price control. If the imbalance is large, the MOC buyer pays whatever price clears it, as the $50.10 example shows.

Finally, trading at the close minimizes tracking error, not cost. The two are different. A fund can track perfectly while paying a temporary premium that reverts overnight.

## Recap

An auction collects orders and executes them all at one price, the one that maximizes matched shares, then minimizes imbalance, then stays close to the mid. Market-on-close orders guarantee participation but give up price, limit-on-close orders control price but may not fill, and imbalance-only orders exist to offset the excess side. Index funds and benchmarked managers concentrate at the close because index levels and NAVs are struck from the closing price, so trading there removes tracking error. From 3:50 p.m., exchanges publish the imbalance, which invites liquidity providers to take the other side of visibly mechanical flow. When that offsetting liquidity is too small, the closing price moves away from the mid and tends to revert after the close, and the tracker pays that cost even though its tracking error looks perfect.

## New Terms

**call auction / single-price auction**: A matching method that collects orders over a period and executes all matched orders at one price.

**market-on-close (MOC)**: An order to trade at the official closing price, whatever it is.

**limit-on-close (LOC)**: An order to trade at the closing price only if it is at or better than a stated limit.

**imbalance-only / closing offset order**: An order that only trades against the side with excess interest, used to offset an imbalance.

**imbalance**: The number of shares on one side of the auction book that cannot be paired with the other side at the reference price.

**paired shares**: Shares that can be matched at the reference price.

**indicative price**: The price at which the auction would clear if it ran with the current book.

**tracking error**: The difference between a fund's return and its benchmark index's return.

**closing price deviation**: The gap between the official closing auction price and the continuous-market midpoint just before the close.

## Questions to Test Yourself

1. Why do many index funds and benchmarked managers trade near the close?

Index levels and fund NAVs are calculated from closing prices, so buying or selling at the close makes the fund's trade price equal to the index's price. Trading earlier creates tracking error in either direction.

2. What is the closing auction trying to solve?

It gives many participants one shared price and pools their orders at one moment. It picks the price that matches the most shares, which is where auction supply and demand cross.

3. Why can auction imbalances move prices?

MOC orders must trade, so if one side has more than the other side's interest near the mid, the price must move until enough contra orders participate. Imbalance publications invite offsetting liquidity, but if too little arrives, the close is pushed away from fair value.

4. What can go wrong if too much flow concentrates in the auction?

The closing price can be distorted by temporary pressure and then revert overnight. The fund's tracking error looks fine, but its investors paid a premium that never shows up in the tracking report.

## Sources

NYSE. "NYSE Auctions: Closing Process Fact Sheet." https://www.nyse.com/publicdocs/nyse/NYSE_Auctions_Closing_Process_Fact_Sheet.pdf

Nasdaq. "Nasdaq Closing Cross Fact Sheet." https://www.nasdaqtrader.com/content/ProductsServices/Trading/Crosses/ccfactsheet.pdf

Nasdaq. "Opening and Closing Crosses FAQ." https://nasdaqtrader.com/content/ProductsServices/Trading/Crosses/openclose_faqs.pdf

Bogousslavsky, Vincent, and Dmitriy Muravyev. "Who Trades at the Close? Implications for Price Discovery, Liquidity, and Disagreement." Working paper, 2020 (AEA 2021). https://aeaweb.org/conference/2021/preliminary/paper/H9T4hef7

Trade Informer. "Nasdaq Closing Cross Handles Record $334 Billion During Russell Rebalance." June 29, 2026. https://www.tradeinformer.com/institutional-trading/nasdaq-closing-cross-handles-record-334-billion-during-russell-rebalance

Petajisto, Antti. 2011. "The Index Premium and Its Hidden Cost for Index Funds." *Journal of Empirical Finance* 18 (2): 271–288. https://petajisto.net/papers/petajisto%202011%20jef%20-%20hidden%20cost%20for%20index%20funds.pdf
