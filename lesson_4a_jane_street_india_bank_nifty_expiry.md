# Lesson 4a: Jane Street in India and Bank Nifty Expiry

## Learning Goal

Lesson 4 said a price can move because someone needs liquidity, not because the company changed. This case is that idea on a settlement. Bank Nifty is a formula of a few bank stocks. Index options expire off that formula. SEBI says Jane Street used large cash and futures prints to move the formula on expiry days so much larger options positions would pay.

This lesson explains the alleged trade, why the economics can work, how the case started, and what the regulator did. It is SEBI's July 3, 2025 interim story, not a final court finding. Jane Street disputes the order.

## The Setup: A Formula, a Thin Leg, a Fat Leg

Bank Nifty (BANKNIFTY) is NSE's bank index. In the period SEBI studied it had twelve constituents. The index level is a weighted average of those stock prices. Weekly index options are contracts on that number. On expiry day they settle from the index, not from a separate "options fair value."

SEBI's own explainer in the order is the key imbalance. On a weekly options expiry, cash-equivalent volume in index options is several times the cash-equivalent volume in the related stocks and futures. January 17, 2024 is their worked day. If you can move the twelve banks a little in cash and stock futures, you move Bank Nifty. The options book on that same day is much larger. A loss on the small, heavy-impact leg can be smaller than the gain on the large, sensitive options leg.

```text
buy / sell the 12 banks (cash + stock futures)
  -> Bank Nifty formula moves
  -> weekly Bank Nifty options settle off that number
  -> options PnL can dwarf the cash/futures PnL
```

That is mechanical in the same sense as Lesson 4. Nobody needs a new fact about HDFC Bank's loans. The index is a rule. Flow in the inputs changes the rule's output.

It is not an index-fund trade. Jane Street was not an index fund that had to own a name. SEBI says the firm *created* the demand shock to move a settlement. Same channel, different intent.

## The Trade SEBI Describes

SEBI calls the main pattern **intraday index manipulation** and walks through January 17, 2024.

**Patch I (morning, about 9:15 to 11:47).** Jane Street entities were the largest net buyer of Bank Nifty constituents in cash and stock futures, about ₹4,370 crore long across those books. They bought all twelve names except Bandhan Bank. At the same time they built a much larger short in Bank Nifty options: buying puts and selling calls. SEBI puts that options short at about ₹32,115 crore cash-equivalent, roughly 7 times the cash-and-futures long.

**Patch II (late morning through the close).** They reversed. They sold the morning's stock and futures, and more, about ₹5,372 crore net sold in SEBI's afternoon tally for the January 17 example. Selling the inputs pushed Bank Nifty down into expiry. The short options book made money as the index fell.

On that day SEBI says the cash-and-futures reversal lost about ₹61.6 crore and the options book made about ₹735 crore. The cash-and-futures book looks irrational by itself. Next to the options book it does not.

```text
morning
  buy the 12 banks (cash + futures)  ->  index up
  buy puts / sell calls              ->  large short on Bank Nifty

afternoon
  sell the 12 banks                  ->  index down into expiry
  options short pays
  cash/futures book can lose
```

SEBI also describes a second pattern, **extended marking the close**: concentrated activity in the last hour on expiry to lean the settlement print in favor of leftover options. Same idea. The close is part of how the formula is fixed that day.

Across 15 expiry days of the first strategy, SEBI says the group took an intraday cash-and-futures loss of about ₹200 crore in order to hold a much larger options edge. Over January 2023 to March 2025 it puts Jane Street's India index-options profit in the tens of thousands of crores, and it treats ₹4,843.57 crore as the unlawful slice it wanted impounded from the 15-day pattern.

## Why It Can Work

The index does not have a separate true price. It is the stocks. Aggressive size in a market that is small next to the options market moves those stocks. Options traders who mark off the live index see a higher (then lower) Bank Nifty and trade against a print that SEBI says was temporary.

A common mistake is to treat the cash-and-futures loss as proof the strategy failed. The cash-and-futures book is the *cost of moving the formula*. The options book is the *bet on the formula*. If the second is several times the first, a planned loss on the first can still be the cheap way to get the second.

That is also why SEBI cares. Moving a public benchmark so your derivatives win, while other people trade the same options, is the line it calls a false appearance of activity. Lesson 3's impact story is the physics. This case is the legal overlay: who is allowed to create that impact on purpose around a settlement.

## How the Case Started and What Happened Next

SEBI did not start from a random scan of Bank Nifty. In April 2024 the press covered Jane Street's U.S. fight with Millennium over India options strategies. SEBI opened a look. NSE was asked to examine the book in July 2024. Jane Street met SEBI in August 2024 and sent a written explanation.

On February 6, 2025, on SEBI's instruction, NSE sent a caution letter: stop large cash-equivalent positions and the patterns NSE flagged. SEBI's order says the group still ran very large expiry-day options risk after that, including in May 2025.

On July 3, 2025 SEBI issued a 105-page interim order (WTM/AN/MRD/MRD-SEC-3/31516/2025-26). It barred JSI Investments, JSI2 Investments, Jane Street Singapore, and Jane Street Asia Trading from accessing the Indian securities market until further orders, and directed that about ₹4,843.57 crore (Reuters: about $567 million) of alleged unlawful gains be impounded into escrow. Open derivatives could be squared in a short window. Reuters reported Jane Street could resume some activity after depositing the money if it dropped the strategy. The firm deposited the sum and said it disputes the findings.

This was an interim restraint and an impound, not a finished trial. Into 2026 Jane Street has been in front of the Securities Appellate Tribunal arguing over documents. Counsel has said NSE and SEBI surveillance patches did not find manipulation in most of the windows they reviewed. That is Jane Street's defense posture. It is not a final verdict.

SEBI also said India-incorporated entities let the group take intraday cash positions that a plain foreign portfolio investor book would have been restricted from. That is a structure point, not the economics of the trade.

## Common Misconceptions

This is not "Jane Street had to buy because it tracks Bank Nifty." The alleged edge is the opposite: create flow so the tracker-like formula moves.

A loss in stocks and futures does not mean the day was a bad hedge. In SEBI's telling it is the admission fee for moving the index.

Options volume being huge in India is background, not a crime. The fight is about using the thin underlying to steer the fat expiry.

Do not treat the ₹4,844 crore figure as a criminal fine already paid in guilt. It is the amount SEBI impounded from its 15-day tally while the case continues.

## Recap

Bank Nifty is a mechanical average of a short list of banks. Weekly options settle off that average. SEBI says Jane Street bought the list hard in the morning, built a much larger short in Bank Nifty options, then sold the list into the close so the index fell and the options paid. The cash-and-futures book can lose. The options book can win by more, because expiry-day options notional is much larger than the underlying. The case began after the Millennium press, ran through an NSE caution, and became a July 2025 interim ban plus a ~₹4,844 crore impound. Jane Street disputes it. For this curriculum the useful residue is the channel: leftover demand in the inputs moves a formula, and a formula is what options expire on.

## New Terms

**Bank Nifty**: NSE's bank-stock index. A weighted formula of its constituents.

**index options expiry**: The day those options settle from the index level, not from a separate options price.

**cash-equivalent options position**: The index exposure implied by an options book, stated like a stock or futures position.

**intraday index manipulation** (SEBI's label): Buy the constituents to lift the index, hold a larger opposite options book, then sell the constituents to mark the index the other way.

**marking the close**: Trading near the close in a way that leans the official settlement print.

**impound**: Regulator-ordered hold of alleged gains, here in escrow, before a final order.

## Questions to Test Yourself

1. What was the trade, in cash, futures, and options?

SEBI says: buy Bank Nifty stocks and stock futures in the morning, build a larger short in Bank Nifty options, then sell the stocks and futures later so the index falls into expiry.

2. Why can buying 12 bank stocks move Bank Nifty?

The index is a weighted formula of those stocks. There is no separate "true" Bank Nifty. Enough size in the inputs moves the output.

3. Why might a loss in cash and futures still be rational?

If options notional is several times the cash-and-futures book, a planned loss on the thin leg can be smaller than the options gain from moving the settlement.

4. What did SEBI do, and is the case closed?

July 2025 interim ban plus about ₹4,844 crore impounded. Jane Street deposited the money, disputes the findings, and has been in SAT on process and documents. No final merits ruling is assumed here.

## Sources

SEBI. Interim Order in the matter of Index manipulation by Jane Street Group. WTM/AN/MRD/MRD-SEC-3/31516/2025-26. July 3, 2025. (NSE circular pointing to the order: https://archives.nseindia.com/content/circulars/INVG68921.pdf)

Reuters. "India bars Jane Street from its securities market, citing manipulation of stock indexes." July 4, 2025. https://www.reuters.com/sustainability/boards-policy-regulation/india-regulator-bars-jane-street-accessing-its-securities-market-2025-07-04/

The Hindu Business Line. "SEBI bars Jane Street from markets, orders impounding ₹4,844 crore in unlawful gains." https://www.thehindubusinessline.com/markets/sebi-bars-jane-street-from-accessing-securities-market/article69771167.ece

The New Indian Express. "Jane Street tells SAT Sebi, NSE probes found no evidence of manipulation." September 4, 2026. https://www.newindianexpress.com/business/2026/Sep/04/jane-street-tells-sat-sebi-nse-probes-found-no-evidence-of-manipulation
