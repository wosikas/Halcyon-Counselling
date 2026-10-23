# FX Trade-Signal Platform: Research Plan

**Goal:** Find out what it would take to build a signal platform (not a broker or execution venue) that flags long and short entries in FX, and related markets, with a measurably better probability of success than what traders can get today. It would combine fundamentals, technicals, mathematical modelling and cross-market correlation.

**The research has to answer four questions:**

1. What already exists, free and paid, and why it is failing traders.
2. Where the real gaps are.
3. Which of those gaps can be filled by an edge we can prove, after trading costs.
4. What the "killer app" is, and what the smallest version of it is that proves the idea.

---

## Guiding principles

- **North Star: 90% accuracy, defined so it can't be gamed.** Hit rate and payoff are mathematically linked. The breakeven win rate is `1 / (1 + R)`, where R is reward-to-risk. So 90% is easy to fake with a tiny target and a wide stop (R = 0.1 breaks even at about 91%), and that loses money once costs are included. The North Star is therefore defined as:
  - **≥ 90% of "A-grade" signals reach target before stop, with reward-to-risk of at least 1:1**, measured live and out-of-sample, after costs, on a published record.
  - **Coverage is reported alongside accuracy:** how many A-grade signals fire per week. The system is allowed, and expected, to say "no trade" most of the time. This approach is called selective prediction, or abstention.
  - **Calibration:** a stated probability of 90% must come true about 90% of the time. Lower tiers (for example 70–80%) are shown honestly as lower tiers.
  - **Expectancy net of spread, slippage and swap** remains the guardrail metric. We also track the R-multiple distribution, maximum adverse and maximum favourable excursion (MAE/MFE), and drawdown.
  - **Reality check:** a sustained 90% at 1:1 would beat every known fund. Renaissance's Medallion fund is reported to be right about 50.75% of the time. The research will establish how close we can get, on which setups, horizons and conditions, and will treat any backtest showing 90%+ as a red flag for overfitting until it is proven live.
  - **Marketing:** public accuracy claims are regulated (UK FCA financial promotions, US FTC/CFTC). We will only claim what the published record shows.
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

## Phase 4: Market-moving activity intelligence ("follow the money and the mouths")

For every source below we record: what it reveals, how delayed it is, how often it updates, cost and licensing, whether we can redistribute it, and **published evidence that it moves or predicts price**. Then we test that ourselves in Phase 8.

### 4a. Large trades and disclosed positions

Spot FX is over-the-counter, so there is no public tape. Large flow still leaks through several disclosure regimes.

| Source | What it shows | Delay |
|---|---|---|
| CFTC Part 43 real-time swap reporting (DTCC public dissemination) | FX options, NDFs and other swaps, including large-notional trades (capped and delayed for block size) | Minutes to hours |
| Large FX option expiries (derived from DTCC data, published daily by news desks) | Big strikes that can pin or attract price around 10am NY cut | Daily |
| CME FX futures and options: block trades, volume, open interest | Large exchange-traded positioning, plus volume and open interest that spot FX lacks | Real-time to end-of-day |
| CFTC Commitments of Traders | Positioning of leveraged funds, asset managers and dealers | Weekly (Tuesday data released Friday) |
| SEC 13F / 13D / 13G, Form 4 insider trades | Holdings of large managers (including sovereign funds that file 13F), 5% stakes, insider buying and selling | 2 business days to 45 days |
| UK and EU major-holding and short-position disclosures | Large stakes and net short positions above thresholds | 1–4 days |
| Japan Ministry of Finance intervention data, central bank FX operations | Official buying and selling of currencies | Monthly, with daily detail later |
| US TIC data, IMF COFER reserves, World Gold Council central bank gold | Foreign official demand for USD, Treasuries and gold | Monthly or quarterly |
| Cross-border M&A announcements | Large deals that require currency conversion | Real-time |
| Calendar flows | Month-end and quarter-end rebalancing, the WM/R 4pm fix, Japanese fiscal half-year repatriation | Predictable dates |

### 4b. Wealthy individuals, companies and sovereign funds

- **Sovereign wealth funds and public pensions:**
  - Norway NBIM holdings, plus Saudi PIF and others through 13F filings
  - Global SWF and SWF Institute trackers
  - announced allocation changes (for example Japan's GPIF)
- **Billionaire and fund-manager moves:** 13F changes for well-known managers, Berkshire filings and letters, hedge fund investor letters, and activist 13D filings.
- **Corporate signals:** insider-trading clusters, large buybacks, and hedging commentary on earnings calls (for example "we expect a stronger dollar to hurt us").

The research question for all of these is honest: most of this data is slow (days to months). It is likely to be useful for **regime and bias** (which way the big money is leaning) rather than for **entry timing**. We will measure that.

### 4c. Politicians, Trump, central bankers and prominent voices

- **Political statements:**
  - Trump's Truth Social posts. There is no official API, so the licensing and terms of service of monitoring services need checking.
  - Posts on X, White House releases and executive orders, and Federal Register tariff notices.
  - Foreign leaders and finance ministries.
- **Precedent:** JPMorgan's 2019 "Volfefe index" showed Trump's tweets measurably moved US rates volatility. Tariff headlines in 2018–19 and 2025 moved CNH, MXN, CAD and EUR.
- **Central bankers:** the speech calendar and transcripts (the BIS central bankers' speeches database), Fed, ECB and BoE minutes, and hawkish/dovish scoring with NLP.
- **Politicians' own trading:** US STOCK Act disclosures, filed within 45 days (via Capitol Trades and Quiver Quantitative style trackers).
- **Prominent investors and institutions:** public commentary from people such as Dalio, Druckenmiller, Ackman and Burry, and from investment banks' public research. Interviews and podcasts can be transcribed. We would measure **each voice's own track record** before giving it any weight.
- **Prediction markets** (Polymarket, Kalshi): live, market-priced probabilities for political events. These are useful for "how much of this is already priced in?"

**Output:** a source inventory with cost, delay and licensing for each, plus a shortlist of 5–10 sources worth testing for predictive value.

## Phase 5: News vs hype vs misdirection ("signal vs noise")

This is about building a way to classify each item as **news**, **hype**, or **misdirection**.

- **What makes something news:**
  - it is new information (novelty detection: not a rehash of yesterday's story)
  - it differs from what was expected (surprise vs consensus, or vs prediction-market odds)
  - it comes from a credible primary source
  - it is confirmed by related markets, for example yields and FX moving together
- **What makes something hype:**
  - mentions accelerate with no confirmation from price, flow or positioning
  - the sources are low-credibility or anonymous
  - the language is promotional, the accounts look like coordinated bots, or the "influencers" have a poor track record
- **What puts traders off the trail:**
  - recycled or stale headlines presented as new
  - a headline that differs from the actual detail of the story
  - fake or impersonation accounts (for example fake breaking-news accounts)
  - "sources say" stories that are later denied
  - crowded retail positioning around obvious levels, which invites stop runs
  - reactions to data that are not justified by the size of the surprise
- **Method:**
  - a source-credibility score and a per-voice accuracy score
  - an LLM-based classifier checked against labelled history
  - "did the market care?" event studies: how much each headline type actually moved price

**Output:** a labelled taxonomy, the scoring design, and an evaluation plan.

## Phase 6: Data and feasibility audit

- **Price data:** OANDA, Dukascopy tick data, LMAX, FXCM, Polygon/Twelve Data, and CME FX futures via Databento. FX futures add volume and open interest, which spot FX does not have.
- **Rates and macro data:** FRED, US Treasury, ECB Data Portal, central bank sites, Trading Economics, Finnhub/FMP calendar APIs.
- **News:** licensed feeds (Benzinga, Newsquawk, RavenPack) vs free sources (GDELT, RSS feeds, central bank releases).
- **Positioning and options data:** CFTC, broker sentiment APIs, DTCC swap data.
- **Licensing for redistribution is the key constraint.** Many feeds forbid showing their data to your customers. Cost each data source at the MVP stage and at scale.
- **Technical needs:** latency budget for each signal type, and the compute needed to run correlation and regime models live.

## Phase 7: Regulatory scan

Find out whether flagging entries counts as regulated investment advice or a "recommendation" in each target market, and what that means for product design (disclaimers, "tool not advice" framing, personalisation limits, marketing rules).

- **UK:** FCA rules on advising, financial promotions and Consumer Duty, plus the FCA's actions against finfluencers.
- **EU:** MiFID II and ESMA investment-recommendation rules.
- **US:** CFTC/NFA rules. Commodity Trading Advisor (CTA) registration can apply to forex advice.
- **Australia and Singapore:** ASIC and MAS.
- **Distribution:** App Store and Google Play rules for financial apps.

## Phase 8: Proof-of-edge experiments (before any build)

Take 3–5 of the strongest hypotheses (including **your correlation method**) and test them honestly on historical data in Python:

- out-of-sample testing, with costs included and calibration measured
- results compared against simple baselines (random entry, buy-and-hold, plain moving-average rules)

Candidate tests:

1. **Lead-lag:** do yield moves or index moves lead specific FX pairs?
2. **Divergence:** when a pair breaks from its usual correlated asset, does it revert or follow through?
3. **Regime filtering:** does a regime filter improve standard technical setups (breakout vs mean-reversion)?
4. **Fundamental bias:** does aligning technical triggers with a macro bias (surprise index plus rate differential) raise expectancy?
5. **Event handling:** does skipping or fading the first move after a data surprise change results?
6. **Big-money and political signals:** do large FX option expiries, COT extremes, block trades or political-statement shocks improve accuracy when combined with the signals above?
7. **The 90% test:** at what confidence threshold, if any, does the combined model reach 90% at 1:1 or better, and how many signals per week survive at that threshold?

**Output:** a short report per test. Kill the ideas that don't hold up.

## Phase 9: UI and dashboard design

- **Teardown of the best interfaces:**
  - Bloomberg Terminal, Koyfin, TradingView, TrendSpider
  - Unusual Whales, Quiver Quantitative, FinancialJuice
  - Forex Factory, Myfxbook
  - what traders praise and hate about each
- **Core screens to prototype:**
  1. **Signal board:** ranked live signals with tier, calibrated probability, entry, stop, target, reasons for and against, and a countdown to the next risk event.
  2. **Cross-asset correlation and lead-lag map:** a live heatmap or network, with divergence alerts highlighted.
  3. **Currency scorecard:** a fundamental bias per currency (surprise index, rate differential, positioning, big-money flow).
  4. **Big-money and political feed:** large trades, option expiries, disclosures, and political or central bank statements. Each item is tagged news, hype or misdirection and shows its measured market impact.
  5. **Event calendar** with expected volatility and prediction-market odds.
  6. **Track record:** every signal ever issued, filterable, with a calibration chart.
- **Alerts:**
  - channels: push, email, Telegram/Discord and webhook
  - filtered by the trader's pairs, tier threshold and prop-firm rules
  - alerts are deliberately few: quality over quantity
- **Process:**
  - wireframes
  - an interactive clickable prototype
  - usability sessions with 5–8 traders

## Phase 10: Gap synthesis and product thesis

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
10. **"Follow the money and the mouths" in one place.** Disclosed big trades, sovereign and billionaire moves, and political and central bank statements, each scored for credibility and measured market impact. Today this information is scattered across a dozen sites.
11. **A noise filter.** Every headline and post is labelled news, hype or misdirection, with the evidence for the label. This directly targets what throws traders off the trail.

## How the work will be executed

- Phases 1–5 run in parallel with research agents, each covering one category, using web search and primary sources. All findings are cited and dated.
- Phase 8 runs in Python notebooks against free or low-cost historical data.
- Deliverables:
  - a research report
  - a source inventory of big-money, political and news feeds
  - a clickable dashboard prototype
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
