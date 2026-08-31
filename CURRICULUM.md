# Curriculum: Market Microstructure, Index Mechanics, and Flows Trading

## Purpose

This curriculum is the persistent learning roadmap for this repository.

The goal is to build practical intuition for market microstructure, index mechanics, index flows, rebalancing, auctions, execution, and flows trading. The repo should help the reader become useful on a flows desk by understanding not only what happens, but why it happens, who is involved, how to estimate the flow, and how to reason about price impact.

Use `AGENTS.md` for the teaching style. Use this file for lesson order, scope, technical prerequisites, and suggested artifacts.

The core question of the repo is:

```text
When a market participant needs to trade, how do we understand the size,
timing, predictability, execution cost, and price effect of that flow?
```

## Source of information

Please write using sources that are high quality or from academic sources that are grounded in truth or studies. Follow Jane st blogs or Optiver or DRW. Read trading firms. Or millenium capital's flows desk. Find real information. We want to learn real things here. Find high quality sources from real trading desks or academic papers or high quality books. Nothing speculative or not real. But high quality information. Site if you need. 

## How to Use This Curriculum

Work through this curriculum one lesson at a time.

For each lesson:

1. Start from the problem the lesson solves.
2. Explain the intuition in plain language.
3. Use a small worked example with numbers.
4. Define the important terminology.
5. Explain the mechanics step by step.
6. Connect the concept to flows trading, index mechanics, execution, or desk decision-making.
7. Include common misconceptions.
8. Include any relevant math, data, or modeling technique.
9. End with a recap and learning checks.

Do not generate multiple full lessons at once unless explicitly requested. The preferred workflow is to create one lesson, review it, improve it, and then move to the next lesson.

## File Naming Convention

Lesson files should live at the repo root unless a later folder structure is created.

Use this filename format:

```text
lesson_x_<short_lowercase_title>.md
```

Use lowercase words separated by underscores.

Examples:

```text
lesson_1_market_participants_and_why_they_trade.md
lesson_2_orders_venues_and_the_limit_order_book.md
lesson_13_estimating_index_flow.md
lesson_24_machine_learning_for_flow_prediction.md
```

## Lesson Format

Each lesson should usually include:

- title
- filename
- learning goal
- why this matters on a flows desk
- first-principles explanation
- small worked example
- key terms
- mechanism walkthrough
- math or data technique, if relevant
- desk intuition
- common misconceptions
- recap
- learning checks
- optional exercises or prompts

Use diagrams when they clarify flows, participant relationships, order books, auctions, index construction, hedging, data pipelines, or feedback loops.

## Curriculum Map

The curriculum is organized into seven tracks:

1. Market structure foundations
2. Microstructure, liquidity, and execution
3. Index construction and index methodology
4. Index adds, deletes, rebalances, and flow prediction
5. ETFs, futures, swaps, and basket trading
6. Math, statistics, and machine learning for flows
7. Case studies and desk-style capstone work

The rough progression is:

```text
participants and orders
  -> liquidity, market impact, and auctions
  -> passive investing and index construction
  -> official methodology rules
  -> adds, deletes, and rebalance timelines
  -> flow estimation and trade prediction
  -> execution and liquidity provision
  -> ETFs, futures, swaps, and baskets
  -> math, statistics, ML, and data pipelines
  -> case studies and capstone rebalance notes
```

## Part 1: Market Participants and Why They Trade

Filename: `lesson_1_market_participants_and_why_they_trade.md`

Learning goal: understand who trades in markets and why their motivations differ.

Focus on asset managers, hedge funds, market makers, dealers, index funds, ETF issuers, retail traders, corporates, arbitrageurs, brokers, transition managers, and exchanges.

Key questions:

- Who is trading because they have a view?
- Who is trading because they must track a benchmark?
- Who is trading because they provide liquidity?
- Who is trading to hedge risk?
- Who is trading because of client demand?
- Who is forced to trade, and who can walk away?

Desk intuition: before analyzing any flow, identify the participant and the reason they must trade.

## Part 2: Orders, Venues, and the Limit Order Book

Filename: `lesson_2_orders_venues_and_the_limit_order_book.md`

Learning goal: understand how orders interact in a market.

Cover market orders, limit orders, bid, ask, spread, displayed liquidity, hidden liquidity, depth, queue priority, exchanges, dark pools, alternative trading systems, and off-exchange trading.

Key questions:

- What is the difference between a market order and a limit order?
- Why does the best bid differ from the best ask?
- What does it mean for liquidity to sit in the book?
- Why can execution price differ from last traded price?
- What changes when an order is routed to a dark pool instead of a lit exchange?

Desk intuition: price is not a single object. The executable price depends on size, urgency, venue, displayed depth, hidden liquidity, and other traders' reactions.

## Part 3: Liquidity, Spreads, Depth, and Market Impact

Filename: `lesson_3_liquidity_spreads_depth_and_market_impact.md`

Learning goal: understand why large or urgent trades move prices.

Cover quoted liquidity, realized liquidity, bid-ask spread, depth, resiliency, temporary impact, permanent impact, participation rate, slippage, and implementation shortfall.

Key questions:

- Why is volume not the same thing as liquidity?
- Why does urgency increase trading cost?
- What makes a trade easy or hard to execute?
- Why can a predictable buyer push prices up before the buyer finishes?
- What is the difference between temporary and permanent price impact?

Math and technique: introduce simple impact scaling, such as comparing expected shares to average daily volume and thinking about nonlinear impact.

Desk intuition: every flow should be compared to available liquidity, not just market cap or daily volume.

## Part 4: Price Formation, Information, and Mechanical Demand

Filename: `lesson_4_price_formation_information_and_mechanical_demand.md`

Learning goal: separate price moves caused by information from price moves caused by trading pressure.

Cover expectations, informed trading, uninformed trading, liquidity demand, mechanical flow, supply and demand, price discovery, and feedback between prices and positioning.

Key questions:

- Did price move because the market learned something?
- Did price move because someone needed liquidity?
- Can information and mechanical pressure both matter?
- How would you distinguish a fundamental repricing from temporary flow pressure?

Desk intuition: "price moved" is not the explanation. The explanation is the mechanism behind the move.

## Part 5: Dealers, Market Makers, and Risk Warehousing

Filename: `lesson_5_dealers_market_makers_and_risk_warehousing.md`

Learning goal: understand how dealers and liquidity providers absorb flow.

Cover principal trading, agency trading, facilitation, inventory, balance sheet, risk limits, hedging, quote adjustment, and compensation for taking risk.

Key questions:

- What happens when a dealer buys what a client sells?
- Why does inventory create risk?
- How might a dealer hedge that risk?
- Why does risk warehousing have a cost?
- Why might dealer appetite change during stress?

Desk intuition: liquidity is often someone else accepting risk temporarily.

## Part 6: Adverse Selection and Market Maker Risk

Filename: `lesson_6_adverse_selection_and_market_maker_risk.md`

Learning goal: understand why liquidity providers worry about trading with better-informed participants.

Cover adverse selection, informed flow, toxic flow, quote widening, spread compensation, latency, news risk, and liquidity withdrawal.

Key questions:

- Why is selling to an informed buyer dangerous?
- Why do spreads widen when uncertainty rises?
- How do market makers protect themselves?
- Why can liquidity disappear when it is most needed?

Desk intuition: liquidity providers care not only about size, but also about whether the other side knows something.

## Part 7: Opening Auctions, Closing Auctions, and Imbalances

Filename: `lesson_7_opening_auctions_closing_auctions_and_imbalances.md`

Learning goal: understand why auctions are central to benchmarked and index-related trading.

Cover opening auctions, closing auctions, market-on-close orders, limit-on-close orders, imbalance messages, indicative match prices, auction collars, benchmark execution, and auction liquidity.

Key questions:

- Why do many index funds and benchmarked managers trade near the close?
- What is the closing auction trying to solve?
- Why can auction imbalances move prices?
- How does benchmark tracking affect execution timing?
- What can go wrong if too much flow concentrates in the auction?

Desk intuition: the close matters because many portfolios are valued and benchmarked against closing prices. Index events often concentrate flow into the closing auction.

## Part 8: Passive Investing, Benchmark Tracking, and Tracking Error

Filename: `lesson_8_passive_investing_benchmark_tracking_and_tracking_error.md`

Learning goal: understand why passive funds trade mechanically.

Cover passive funds, index funds, benchmarked active funds, tracking error, cash drag, sampling, full replication, optimization, and rules-based trading.

Key questions:

- Why does an index fund buy or sell without a view on valuation?
- What is tracking error?
- Why does benchmark tracking create predictable trades?
- Why are passive flows important even if they are not informed?
- Why might a fund not perfectly replicate its benchmark?

Desk intuition: passive does not mean inactive. Passive rules can create large required trades.

## Part 9: Index Construction Basics

Filename: `lesson_9_index_construction_basics.md`

Learning goal: understand how index methodology turns company data into portfolio weights.

Cover market capitalization, shares outstanding, free float, float adjustment, investable market capitalization, price return, total return, equal weighting, market-cap weighting, liquidity screens, size screens, and eligibility rules.

Key questions:

- What determines a company's weight in an index?
- Why does free float matter?
- How does market-cap weighting differ from equal weighting?
- Why do index rules create mechanical trading consequences?
- What company data matters most for index inclusion?

Math and technique: calculate market cap, float-adjusted market cap, and index weight for a three-stock toy index.

Desk intuition: index methodology converts public company facts into target portfolio weights.

## Part 10: Index Divisors, Corporate Actions, and Continuity

Filename: `lesson_10_index_divisors_corporate_actions_and_continuity.md`

Learning goal: understand how indexes stay continuous through corporate events.

Cover index level calculation, divisors, stock splits, special dividends, ordinary dividends, mergers, spin-offs, rights offerings, share changes, float changes, and divisor adjustments.

Key questions:

- Why does an index need a divisor?
- How can a stock split leave index value unchanged?
- Which corporate actions change index weights?
- Which corporate actions create actual trading needs?
- Why is continuity different from required rebalance flow?

Math and technique: work through a simple divisor adjustment after a stock split or special dividend.

Desk intuition: some index changes are accounting adjustments, while others force portfolios to buy or sell.

## Part 11: Official Index Methodology Documents

Filename: `lesson_11_official_index_methodology_documents.md`

Learning goal: learn how to read the documents that determine index membership and rebalance flow.

Cover methodology guides, ground rules, eligibility criteria, buffer rules, review calendars, announcement dates, implementation dates, free-float rules, liquidity screens, investability screens, country classification, and treatment of corporate actions.

Documents and sources to study:

- FTSE Russell US Equity Indexes Ground Rules
- Russell US Indexes annual reconstitution methodology and calendar
- S&P U.S. Indices Methodology
- S&P Dow Jones Indices Index Mathematics Methodology
- MSCI Global Investable Market Indexes Methodology
- MSCI Global Investable Market Indexes methodology booklets and corporate events methodology
- CRSP US Equity Indexes methodology, especially because Vanguard uses CRSP indexes for some funds
- Vanguard fund documents and benchmark descriptions for understanding what index a fund tracks
- BlackRock iShares ETF prospectuses, holdings files, and creation/redemption basket information when available
- Exchange auction documentation from NYSE and Nasdaq

Key questions:

- What are the index eligibility rules?
- What are the review dates and implementation dates?
- Are there buffers that reduce turnover?
- How are float, shares, and liquidity measured?
- What is announced in advance?
- What must be inferred?

Desk intuition: the methodology document is the rulebook. If you can translate rules into expected trades, you can add value.

## Part 12: Index Adds, Deletes, and Weight Changes

Filename: `lesson_12_index_adds_deletes_and_weight_changes.md`

Learning goal: understand why index membership and weight changes create flow.

Cover additions, deletions, migrations, size bands, buffer zones, liquidity thresholds, free-float changes, share updates, corporate action-driven changes, and index family migrations.

Key questions:

- Why does adding a stock create buying pressure?
- Why does deleting a stock create selling pressure?
- How do buffer rules reduce turnover?
- Why can weight changes matter even without adds or deletes?
- Why might small-cap, mid-cap, and large-cap index changes interact?

Desk intuition: the trade is often not "is this company good?" but "how many shares must index-linked holders buy or sell?"

## Part 13: Rebalance Timelines, Announcements, and Event Windows

Filename: `lesson_13_rebalance_timelines_announcements_and_event_windows.md`

Learning goal: understand the sequence of events around an index rebalance.

Cover estimation windows, rank dates, announcement dates, effective dates, implementation dates, transition periods, review cycles, closing auctions, and post-event windows.

Key questions:

- When does the market learn the likely change?
- When do passive funds need to be aligned?
- When do arbitrageurs start positioning?
- Why can price move before the actual rebalance?
- What happens between announcement and implementation?

Desk intuition: timing matters because predictable future flow can become today's trade.

## Part 14: Estimating Index Flow

Filename: `lesson_14_estimating_index_flow.md`

Learning goal: estimate the size and direction of required index-related trades.

Cover assets tracking an index, benchmarked assets, target weights, current weights, float-adjusted market cap, price, shares to trade, dollar flow, average daily volume, auction volume, days-to-trade, and liquidity scaling.

Key questions:

- How much money tracks the index?
- What is the current weight?
- What is the target weight?
- How many dollars need to trade?
- How many shares does that represent?
- How large is that trade relative to normal volume and auction volume?

Math and technique: calculate expected dollar flow and shares to trade:

```text
target_dollars = index_tracking_aum * target_weight
current_dollars = index_tracking_aum * current_weight
dollar_flow = target_dollars - current_dollars
shares_to_trade = dollar_flow / stock_price
flow_as_adv = shares_to_trade / average_daily_volume
```

Desk intuition: flow estimation turns index methodology into expected buy and sell pressure.

## Part 15: Predicting Index Adds and Deletes

Filename: `lesson_15_predicting_index_adds_and_deletes.md`

Learning goal: learn how traders forecast index changes before official announcements.

Cover rank-day prediction, market-cap cutoffs, buffer rules, eligibility screens, IPO seasoning, profitability rules, liquidity screens, float updates, corporate actions, and index committee discretion.

Key questions:

- Which stocks are close to the inclusion or deletion threshold?
- What data inputs determine eligibility?
- Which inputs are uncertain before announcement?
- How do buffers change the prediction problem?
- How should predictions be expressed as probabilities rather than certainties?

Math and technique: build a simple rules-based classifier that labels likely adds, likely deletes, and borderline names.

Desk intuition: being useful means knowing not only the likely changes, but also which predictions are fragile.

## Part 16: Pre-Positioning, Crowding, and Reversal

Filename: `lesson_16_pre_positioning_crowding_and_reversal.md`

Learning goal: understand how traders anticipate predictable flows and why the trade can get crowded.

Cover pre-positioning, event-driven trading, expected flow, crowding, borrow constraints, short interest, liquidity supply, risk transfer, convergence, and post-event reversal.

Key questions:

- Who can predict the rebalance flow?
- Why might traders buy before index funds buy?
- What happens if too many traders pre-position?
- Why might the price reverse after implementation?
- How can you distinguish flow realization from flow exhaustion?

Desk intuition: a predictable flow can be valuable, but only if it is not already crowded and priced in.

## Part 17: Liquidity Provision Around Rebalances

Filename: `lesson_17_liquidity_provision_around_rebalances.md`

Learning goal: understand who takes the other side of rebalance trades.

Cover liquidity providers, dealers, market makers, transition managers, agency execution, principal facilitation, risk transfer, auction participation, and price concessions.

Key questions:

- Who sells to passive buyers?
- Who buys from passive sellers?
- What price concession do liquidity providers require?
- Why does liquidity provision depend on risk and timing?
- How do dealers manage the risk of providing liquidity into a known event?

Desk intuition: rebalance execution is partly a search for enough liquidity at an acceptable price.

## Part 18: Execution Algorithms and Trading Benchmarks

Filename: `lesson_18_execution_algorithms_and_trading_benchmarks.md`

Learning goal: understand how large orders are executed and measured.

Cover VWAP, TWAP, arrival price, implementation shortfall, participation rate, POV algorithms, liquidity-seeking algorithms, market-on-close execution, limit-on-close execution, and benchmark risk.

Key questions:

- What benchmark is the trader trying to beat?
- Why can a trade look good versus VWAP and bad versus arrival price?
- How does urgency affect execution cost?
- How does an execution algorithm balance price, size, and completion risk?

Desk intuition: good execution depends on the objective. A rebalance trade may care more about closing-price tracking than intraday alpha.

## Part 19: ETFs, Creation/Redemption, and Basket Trading

Filename: `lesson_19_etfs_creation_redemption_and_basket_trading.md`

Learning goal: understand how ETF trading connects to underlying basket flow.

Cover ETF shares, NAV, intraday indicative value, premiums, discounts, authorized participants, creation units, redemptions, custom baskets, basket liquidity, and ETF arbitrage.

Key questions:

- Why can an ETF trade away from NAV?
- How do authorized participants arbitrage ETF mispricing?
- When does ETF trading create underlying stock flow?
- How do baskets make trading more efficient?
- Why might ETF stress affect underlying liquidity?

Desk intuition: ETF flow may or may not immediately become underlying stock flow. The creation/redemption mechanism determines the link.

## Part 20: Futures, Swaps, Program Trading, and Portfolio Trades

Filename: `lesson_20_futures_swaps_program_trading_and_portfolio_trades.md`

Learning goal: understand instruments used to move index and basket risk efficiently.

Cover index futures, total return swaps, baskets, program trades, portfolio trades, beta hedging, basis, fair value, financing, dividends, and tracking error.

Key questions:

- Why trade futures instead of every stock in an index?
- What risk remains when hedging a basket with a future?
- What is basis?
- How do swaps transfer index exposure?
- Why might a desk use futures first and cash equities later?

Desk intuition: flows desks often manage exposure first and fine-tune individual names later.

## Part 21: Portfolio Math for Index and Flow Trading

Filename: `lesson_21_portfolio_math_for_index_and_flow_trading.md`

Learning goal: learn the math needed to reason about baskets, weights, returns, exposures, and hedges.

Cover weights, returns, log returns, arithmetic returns, portfolio return, beta, covariance, correlation, factor exposure, tracking error, and active weights.

Key questions:

- How do individual stock returns combine into portfolio return?
- What does a portfolio weight mean?
- What is active weight versus benchmark weight?
- How do beta and factor exposure affect hedging?
- What does tracking error measure?

Math and technique: use vectors for weights and returns:

```text
portfolio_return = weight_vector dot return_vector
active_weight = portfolio_weight - benchmark_weight
tracking_error depends on active weights and the covariance matrix
```

Desk intuition: linear algebra shows up naturally because baskets are vectors of positions, weights, returns, and risks.

## Part 22: Probability, Statistics, and Event Studies

Filename: `lesson_22_probability_statistics_and_event_studies.md`

Learning goal: learn the statistical tools needed to study flow events.

Cover distributions, expected value, variance, covariance, correlation, z-scores, confidence intervals, hypothesis testing, event windows, abnormal returns, cumulative abnormal returns, and selection bias.

Key questions:

- Did a stock move unusually around an index event?
- What is the normal return benchmark?
- How do we compare event names to non-event names?
- What is the risk of overfitting one historical pattern?
- How do we separate signal from noise?

Math and technique: build a simple event study around announcement date and effective date.

Desk intuition: event studies help test whether a flow pattern is real, but they can be misleading if the sample is biased or regimes change.

## Part 23: Calculus, Optimization, and Market Impact Models

Filename: `lesson_23_calculus_optimization_and_market_impact_models.md`

Learning goal: understand the math behind execution tradeoffs.

Cover cost functions, marginal cost, convexity, constraints, optimization, risk versus cost tradeoff, temporary impact, permanent impact, and simple optimal execution intuition.

Key questions:

- Why might impact increase nonlinearly with trade size?
- What is the marginal cost of trading faster?
- Why does spreading a trade over time reduce impact but increase price risk?
- What does an execution optimizer try to minimize?

Math and technique: introduce simple cost minimization with constraints:

```text
total_cost = expected_impact_cost + risk_cost + fees
```

Desk intuition: execution is an optimization problem under uncertainty, liquidity limits, and time pressure.

## Part 24: Data Engineering for Flow Research

Filename: `lesson_24_data_engineering_for_flow_research.md`

Learning goal: understand the data pipelines needed to research index flows and market microstructure.

Cover prices, volumes, corporate actions, shares outstanding, free float, index membership, index weights, ETF holdings, fund AUM, auction imbalance data, borrow data, short interest, security identifiers, and point-in-time data.

Key questions:

- What data is needed to estimate flow?
- Which data must be point-in-time to avoid lookahead bias?
- How do corporate actions affect historical calculations?
- How do ticker changes, mergers, and share changes break naive datasets?
- What should a daily rebalance research pipeline produce?

Pipeline idea:

```text
raw vendor files
  -> clean identifiers
  -> adjust corporate actions
  -> build point-in-time universe
  -> compute index weights and changes
  -> estimate expected flows
  -> join liquidity and price data
  -> produce signals and reports
```

Desk intuition: a good flow model is only as good as its data timing, identifiers, and corporate action handling.

## Part 25: Machine Learning for Flow Prediction

Filename: `lesson_25_machine_learning_for_flow_prediction.md`

Learning goal: understand where machine learning can help and where rules-based modeling is better.

Cover classification, regression, ranking, probability calibration, feature engineering, train/test splits, walk-forward validation, leakage, cross-validation for time series, model interpretability, and model monitoring.

Possible ML tasks:

- predict likely index additions and deletions
- estimate probability of borderline index inclusion
- predict flow size conditional on inclusion
- predict price impact around announcement or implementation
- classify crowded versus uncrowded flow events
- forecast auction imbalance direction or magnitude

Key questions:

- Is this a rules problem, a prediction problem, or both?
- What features are known before the event?
- What target are we predicting?
- How do we avoid lookahead bias?
- How do we evaluate the model in a way that matches desk decisions?

Desk intuition: ML can help rank uncertainty and detect patterns, but index methodology is often rules-based. Do not use ML where the rulebook already gives the answer.

## Part 26: Signals, Backtesting, and Research Hygiene

Filename: `lesson_26_signals_backtesting_and_research_hygiene.md`

Learning goal: learn how to test a flow signal without fooling yourself.

Cover signal construction, forward returns, transaction costs, borrow costs, capacity, slippage, survivorship bias, lookahead bias, data snooping, regime changes, feature stability, and out-of-sample testing.

Key questions:

- When would the signal have been known?
- Can the strategy trade enough size?
- What transaction costs would it pay?
- Does the signal survive after costs?
- Is the result driven by a few events?
- Does the signal still work after the market learns it?

Desk intuition: a backtest is not a PnL machine. It is a tool for checking whether a market intuition survives contact with data.

## Part 27: Reading List and Source Documents

Filename: `lesson_27_reading_list_and_source_documents.md`

Learning goal: build a map of primary sources and references worth reading.

Official methodology and market-structure documents:

- FTSE Russell US Equity Indexes Ground Rules
- Russell US Indexes annual reconstitution schedule and methodology notes
- S&P U.S. Indices Methodology
- S&P Dow Jones Indices Index Mathematics Methodology
- MSCI Global Investable Market Indexes Methodology
- MSCI corporate events methodology documents
- CRSP US Equity Indexes methodology
- Vanguard fund prospectuses, annual reports, and benchmark descriptions
- BlackRock iShares ETF prospectuses, holdings files, and creation/redemption education material
- NYSE auction and imbalance documentation
- Nasdaq opening and closing cross documentation
- SEC market structure releases and investor bulletins when relevant

Books and broad references:

- Trading and Exchanges by Larry Harris
- Market Microstructure in Practice by Laruelle, Lehalle, and Pages
- Algorithmic and High-Frequency Trading by Cartea, Jaimungal, and Penalva
- Active Portfolio Management by Grinold and Kahn
- Advances in Financial Machine Learning by Marcos Lopez de Prado, with caution and emphasis on leakage avoidance

Key questions:

- Which sources define rules?
- Which sources explain mechanisms?
- Which sources are vendor or product-specific?
- Which sources are academic and may need practical interpretation?

Desk intuition: primary methodology documents are often more valuable than summaries because small rule details can drive large flows.

## Part 28: Capstone Rebalance and Flow Trading Playbook

Filename: `lesson_28_capstone_rebalance_and_flow_trading_playbook.md`

Learning goal: produce a desk-style rebalance note and research workflow.

The final project should produce a written rebalance note that includes:

- event summary
- relevant index methodology
- expected additions, deletions, migrations, and weight changes
- estimated dollars and shares to trade
- flow as a percentage of average daily volume
- flow as a percentage of expected auction volume
- liquidity conditions
- borrow and short-interest considerations
- likely participants
- likely pre-positioning
- execution timing
- auction considerations
- ETF, futures, swap, or basket hedging considerations
- risks to the thesis
- expected post-event behavior
- what would invalidate the analysis

Capstone workflow:

```text
read methodology
  -> identify candidate changes
  -> estimate probabilities
  -> calculate expected weights
  -> estimate flow in dollars and shares
  -> compare flow to liquidity
  -> analyze crowding and positioning
  -> plan execution or risk transfer
  -> monitor announcement and auction data
  -> review realized price impact
```

Desk intuition: the goal is to move from "an index rebalance happened" to "here is who needs to trade, when, how much, why price may move, what is already priced in, and what could go wrong."

## Math and Technical Prerequisites

The useful math is practical rather than abstract.

Linear algebra matters because portfolios are vectors:

- weights
- positions
- returns
- factor exposures
- active weights
- covariance matrices
- hedge ratios

Probability and statistics matter because flow trading involves uncertainty:

- event probabilities
- expected value
- variance
- correlations
- confidence intervals
- event studies
- regression
- classification
- calibration

Calculus and optimization matter for execution:

- marginal cost
- convex cost curves
- risk versus impact tradeoffs
- constrained optimization
- minimizing expected trading cost

Machine learning matters when the problem has uncertainty and many features:

- predicting borderline index additions or deletions
- estimating event probabilities
- ranking likely high-impact flows
- forecasting auction imbalances
- detecting crowding
- modeling post-event reversal

But rules come first. If the methodology document gives a deterministic answer, use the rules. Use ML where the answer is uncertain, noisy, delayed, or dependent on many interacting variables.

## Suggested Repo Artifacts

Over time, this repo can grow into a practical learning and research workspace.

Useful files and folders:

```text
README.md
AGENTS.md
CURRICULUM.md
glossary.md
questions.md
reading_list.md
lessons/
case_studies/
notebooks/
data_notes/
flow_models/
rebalance_playbooks/
```

Possible projects:

- toy index weight calculator
- rebalance flow estimator
- add/delete prediction checklist
- Russell reconstitution candidate tracker
- closing auction explainer
- ETF creation/redemption explainer
- event study notebook
- simple price impact model
- ML pipeline sketch for flow prediction
- capstone rebalance note template

## Default Prompt for Creating a Lesson

Use a prompt like this when asking an agent to write a lesson:

```text
Use @AGENTS.md and @CURRICULUM.md.

Create Lesson [number] only: [lesson title].

Name the file lesson_[number]_[short_lowercase_title].md, using underscores instead of spaces.

Follow the teaching style in AGENTS.md. Start from first principles, explain the problem, give intuition, use a small worked example, define jargon plainly, connect the topic to flows trading or index mechanics, include relevant math or data techniques, include misconceptions, and end with a recap and learning checks.

Do not create later lessons yet.
```

## Progress Rule

Build this curriculum in small steps.

Do not try to complete the whole repository at once. Create one lesson, review it, revise it, and then proceed to the next lesson.
