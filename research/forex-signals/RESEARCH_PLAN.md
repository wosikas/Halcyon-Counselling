# FX Trade-Signal Platform: Research Plan

**Goal:** Find out what it would take to build a signal platform (not a broker or execution venue) that flags long and short entries in FX, and related markets, with a measurably better probability of success than what traders can get today. It would combine fundamentals, technicals, mathematical modelling and cross-market correlation.

**The research has to answer four questions:**

1. What already exists, free and paid, and why it is failing traders.
2. Where the real gaps are.
3. Which of those gaps can be filled by an edge we can prove, after trading costs.
4. What the "killer app" is, and what the smallest version of it is that proves the idea.

---

## Guiding principles

- **Define "higher probability" before anything else.** Hit rate alone is misleading. A 70% win rate with a 1:0.3 reward-to-risk loses money. Every claim will be judged on **expectancy net of spread, slippage and swap**. We will also track R-multiple distribution, maximum adverse and maximum favourable excursion (MAE/MFE), drawdown, and **calibration**: when we say 65%, it should happen about 65% of the time.
- **Assume nothing is an edge until tested out-of-sample.** Most signal products fail through overfitting and survivorship bias. The research will apply the same tests to our own ideas as to competitors'.
- **Evidence, not opinion.** Every competitor claim, price and feature gets a source and a date. User pain points come from real reviews and forums, not assumptions.
- **Regulation shapes the product.** Whether this is "advice" or "information/tools" changes what we can build and say. This gets checked early, not at launch.

---

## Phase 0: Framing (with you)

- Capture your own experience: which tools you have used, why they failed, and **your correlation method in detail**. This is the core intellectual property, so we codify it first and test it later.
- Lock down scope:
  - **Instruments:** FX majors and crosses, plus gold, oil, indices, bond yields and crypto as cross-asset inputs.
  - **Timeframes:** scalping, intraday or swing.
  - **Target users:** retail day traders, swing traders, prop-firm challenge traders, or semi-professionals.
  - **Jurisdictions:** which countries we sell into.
- Write down falsifiable hypotheses, for example: "US 2-year yield moves lead USD/JPY intraday by X minutes, and that is tradeable net of costs."

## Phase 1: Competitive landscape census

A structured catalogue of every meaningful tool. For each one we record: price, features, data sources, latency, instruments, how signals are delivered, whether the track record is verifiable, business model (including broker affiliate or IB conflicts of interest), user ratings and complaints, and regulatory posture.

| Category | Examples to cover (non-exhaustive) |
|---|---|
| Signal services and Telegram/Discord groups | ForexSignals.com, Learn2Trade, 1000pip Builder, large Telegram channels, MQL5 Signals |
| Copy and social trading | eToro CopyTrader, ZuluTrade, Myfxbook AutoTrade, Darwinex, cTrader Copy |
| Charting and scripting platforms | TradingView (Pine Script, alerts, Ideas), MetaTrader 4/5 and the MQL5 Market, cTrader, NinjaTrader |
| Automated technical analysis and pattern recognition | Autochartist, Trading Central, TrendSpider, Tickeron, Acuity Trading |
| Sentiment and positioning | IG client sentiment, Myfxbook community outlook, OANDA order book, Dukascopy SWFX, CFTC COT reports |
| News and squawk | FinancialJuice, ForexLive, Newsquawk, LiveSquawk, RANsquawk, Benzinga Pro, Bloomberg / LSEG Workspace |
| Economic calendars and macro data | Forex Factory, Investing.com, Trading Economics, Myfxbook calendar, CME FedWatch |
| Macro and fundamental scoring | EdgeFinder-style currency scorecards, FXStreet, Macro Hive, Spectra Markets (AM/FX), bank research portals |
| Correlation tools | Myfxbook, Mataf, OANDA, Babypips and TradingView correlation indicators |
| Journaling and analytics | Edgewonk, TradeZella, TraderSync, FX Blue, Myfxbook (these hold outcome data and are a possible partner or competitor) |
| "AI" signal apps and newcomers | LLM news summarisers, AI chart readers, app-store "AI signals" apps |
| Institutional benchmark (what pros get) | RavenPack, Bloomberg FX forecasts, rates-implied central bank paths, FX factor indices (carry, momentum, value) |

**Output:** a competitor matrix (spreadsheet) and a short profile of the 15–20 most relevant players.

## Phase 2: Voice of the customer (why traders say these tools fail)

- Mine Reddit (r/Forex, r/Daytrading, r/Trading), Forex Factory forums, Trustpilot, App Store and Google Play reviews, YouTube comments, and prop-firm Discords.
- Code the complaints into themes and count how often each comes up.
- Optional: run 10–20 short interviews or a survey with traders you know.

**Failure modes to test for:**

- Unverifiable or cherry-picked results
- Signals with no reasoning and no invalidation level
- Signals that lag or arrive late
- Too many alerts
- No sense of market regime
- Blindness to news events
- No guidance on position sizing or risk
- Conflicts of interest (providers paid on client losses through broker affiliation)
- Chat rooms dominated by noise and self-proclaimed gurus

## Phase 3: Mathematical modelling and quant literature review

Review academic and practitioner work (SSRN, arXiv q-fin, BIS and central bank papers, López de Prado, Ernie Chan, Kaufman) across:

- **Co-movement and correlation, done properly:**
  - rolling and EWMA correlation, and DCC-GARCH dynamic correlation
  - detecting correlation breakdowns and regime changes
  - cointegration (Engle-Granger, Johansen) for pairs and currency triangles
  - PCA and factor decomposition (USD factor, risk-on/risk-off factor)
  - correlation networks (minimum spanning trees)
  - currency-strength indices built from proper baskets
- **Lead-lag between markets:**
  - cross-correlation at lags, Granger causality, transfer entropy
  - asynchronous-data estimators (Hayashi-Yoshida)
- **Cross-market drivers:**
  - rate differentials (2-year spreads) feeding into FX
  - equities and VIX as a read on risk appetite
  - commodity links: oil → CAD/NOK, gold and iron ore → AUD, dairy → NZD
  - credit spreads and crypto
- **Regime detection:** hidden Markov and Markov-switching models, GARCH-family and realised volatility, change-point detection.
- **Fundamentals made quantitative:**
  - economic surprise indices (actual vs consensus, normalised)
  - event studies of how price reacts to data releases
  - market-implied central bank paths
  - NLP on central bank speeches and news
- **Known FX risk premia:** carry, time-series and cross-sectional momentum, value (PPP/REER), the dollar factor, and the volatility risk premium.
- **Microstructure signals retail traders can access:** session opens, the WM/R 4pm fix, large option expiries (DTCC data), retail positioning as a contrarian signal, CFTC COT.
- **Turning signals into probabilities:**
  - triple-barrier labelling and meta-labelling
  - probability calibration and conformal prediction
  - Bayesian updating as evidence arrives
  - fractional-Kelly position sizing
- **Validation rigour:**
  - walk-forward testing and purged / combinatorial cross-validation
  - deflated Sharpe ratio and probability of backtest overfitting
  - multiple-testing corrections (White's Reality Check, Hansen's SPA test)

**Output:** a ranked list of modelling techniques. For each one: what it would add to the product, what data it needs, how hard it is to build, and the evidence that it works.

## Phase 4: Data and feasibility audit

- **Price data:** OANDA, Dukascopy tick data, LMAX, FXCM, Polygon/Twelve Data, and CME FX futures via Databento. FX futures add volume and open interest, which spot FX does not have.
- **Rates and macro data:** FRED, US Treasury, ECB Data Portal, central bank sites, Trading Economics, Finnhub/FMP calendar APIs.
- **News:** licensed feeds (Benzinga, Newsquawk, RavenPack) vs free sources (GDELT, RSS feeds, central bank releases).
- **Positioning and options data:** CFTC, broker sentiment APIs, DTCC swap data.
- **Licensing for redistribution is the key constraint.** Many feeds forbid showing their data to your customers. Cost each data source at the MVP stage and at scale.
- **Technical needs:** latency budget for each signal type, and the compute needed to run correlation and regime models live.

## Phase 5: Regulatory scan

Find out whether flagging entries counts as regulated investment advice or a "recommendation" in each target market, and what that means for product design (disclaimers, "tool not advice" framing, personalisation limits, marketing rules).

- **UK:** FCA rules on advising, financial promotions and Consumer Duty, plus the FCA's actions against finfluencers.
- **EU:** MiFID II and ESMA investment-recommendation rules.
- **US:** CFTC/NFA rules. Commodity Trading Advisor (CTA) registration can apply to forex advice.
- **Australia and Singapore:** ASIC and MAS.
- **Distribution:** App Store and Google Play rules for financial apps.

## Phase 6: Proof-of-edge experiments (before any build)

Take 3–5 of the strongest hypotheses (including **your correlation method**) and test them honestly on historical data in Python:

- out-of-sample testing, with costs included and calibration measured
- results compared against simple baselines (random entry, buy-and-hold, plain moving-average rules)

Candidate tests:

1. **Lead-lag:** do yield moves or index moves lead specific FX pairs?
2. **Divergence:** when a pair breaks from its usual correlated asset, does it revert or follow through?
3. **Regime filtering:** does a regime filter improve standard technical setups (breakout vs mean-reversion)?
4. **Fundamental bias:** does aligning technical triggers with a macro bias (surprise index plus rate differential) raise expectancy?
5. **Event handling:** does skipping or fading the first move after a data surprise change results?

**Output:** a short report per test. Kill the ideas that don't hold up.

## Phase 7: Gap synthesis and product thesis

- A gap matrix scoring each capability (rows) against each competitor (columns).
- Opportunities scored on: how painful the problem is for traders, whether we can prove an edge, whether it is defensible, data cost, regulatory risk, and willingness to pay.
- A killer-app concept, an MVP scope, the business model, the moat, and the top risks.

---

## Early gap hypotheses (to be validated, not assumed)

1. **Trust:** a public, tamper-evident record of every signal ever issued, losers included, with no deleting. Almost nobody does this.
2. **Context over calls:** every signal comes with why it fired, the invalidation level, the current regime, the evidence against it, and a calibrated probability rather than an arrow.
3. **A cross-asset confluence engine:** dynamic correlation, lead-lag and divergence alerts. Today's correlation tools are mostly static Pearson tables.
4. **A fundamentals-to-technicals bridge:** a live macro scorecard per currency, driven by data surprises and rate expectations, sets the directional bias. Technicals only time the entry.
5. **Event awareness:** pre-release risk flags, plus post-release analysis of whether the reaction matched the size of the surprise.
6. **Personalisation from the trader's own journal:** a read-only link to MT4/5 or cTrader learns which setups this trader actually executes profitably, and filters signals to match.
7. **Better trading chat rooms:** calls posted in a structured format, reputation earned from verified outcomes, and AI summaries of the room. This removes the guru noise.
8. **Prop-firm-aware risk:** signals and position sizes that respect the trader's challenge rules (daily loss and maximum drawdown limits). This is a large, underserved segment.
9. **Fewer, ranked alerts** instead of a firehose.

## How the work will be executed

- Phases 1–3 run in parallel with research agents, each covering one category, using web search and primary sources. All findings are cited and dated.
- Phase 6 runs in Python notebooks against free or low-cost historical data.
- Deliverables:
  - a research report
  - the competitor matrix
  - the backtest notebooks
  - a product thesis and MVP specification

## Open questions for you

1. What does "dtds" mean? Day traders? Another instrument or product type?
2. Which countries or regulators will you sell into?
3. Can you describe your correlation approach: which instruments, which timeframes, and what you look for?
4. Which tools have you used, and what specifically went wrong with each?
5. Which trading styles and timeframes are you targeting?
6. What is your budget for market and news data, roughly: free only, under $500/month, or more?
