# Sentinel 2.0

**Sentinel 2.0** is a research-grade Python CLI for studying how online attention, sentiment, narrative coordination, and alternative data relate to stock and crypto price behavior.

It started as a simple “Reddit + Twitter mention counter.”  
It is now designed as a **full market-intelligence and event-analysis platform** for:

- collecting social and market data,
- normalizing it into a consistent schema,
- extracting sentiment and attention features,
- aligning those features with market regimes,
- running lead/lag and event studies,
- and eventually producing reproducible signals, reports, and backtests.

---

## Why this project exists

This project is built to mirror the way serious market-data and quant-adjacent teams think:

- **Alternative data ingestion**
- **Feature engineering**
- **Event-driven analysis**
- **Lead/lag testing**
- **Signal validation**
- **Backtesting with realistic assumptions**
- **Reproducible pipelines and reporting**

The goal is not to build a meme dashboard.

The goal is to build a **professional portfolio project** that demonstrates strong ability in:

- Python engineering
- CLI design
- data modeling
- market data workflows
- NLP pipelines
- analytics and experimentation
- software quality and repo design

---

## What Sentinel 2.0 is evolving into

Sentinel 2.0 is planned as a modular system with the following layers:

### 1. Data ingestion
Collect data from sources such as:

- Reddit
- X / Twitter
- Google Trends
- market price/volume feeds
- optional future sources like news headlines, SEC filings, and Discord/YouTube transcripts

### 2. Normalization
Convert source-specific records into a shared event schema so downstream analysis does not care where a signal came from.

### 3. NLP + narrative intelligence
Go beyond raw mention counts:

- polarity / sentiment scoring
- finance-aware sentiment models
- ticker extraction
- spam/noise reduction
- topic clustering
- narrative persistence
- burst detection
- coordinated hype detection

### 4. Feature engineering
Build features that matter more than “number of mentions”:

- mention velocity
- sentiment momentum
- unique author counts
- post-to-comment ratios
- engagement-weighted sentiment
- z-scored attention spikes
- time-bucketed abnormal activity
- cross-platform confirmation
- social signal divergence vs price action

### 5. Market alignment
Merge alternative data with market structure:

- returns
- abnormal returns
- realized volatility
- intraday / daily volume changes
- pre/post-event windows
- rolling beta and regime context
- comparison to benchmark or sector ETF

### 6. Analytics
Support research-style analyses such as:

- correlation matrices
- lead/lag analysis
- event studies
- Granger-style predictive tests
- cross-sectional ranking
- signal decay analysis
- false-positive analysis

### 7. Backtesting
Later stages can evaluate whether a derived signal has economic value after:

- slippage
- commissions
- delayed execution assumptions
- walk-forward evaluation
- out-of-sample testing

### 8. Reporting
Produce terminal-friendly and exportable outputs:

- rich console summaries
- markdown research reports
- JSON outputs for downstream tooling
- HTML reports later

---

## Current direction

This repo is being structured in a way that is:

- **production-minded**
- **solo-developer manageable**
- **easy to extend**
- **good on a resume**
- **good for learning real workflows**

The immediate bootstrap phase focuses on:

- package structure
- settings/config management
- installable CLI
- environment handling
- versioning
- developer tooling

---

## Planned architecture

```text
src/sentinel/
├── cli/            # Typer CLI entrypoints and commands
├── connectors/     # Reddit, X, Trends, future data adapters
├── market/         # Price/volume and market context clients
├── instruments/    # Ticker resolution, symbol parsing, mappings
├── nlp/            # Sentiment, text normalization, topic features
├── features/       # Feature engineering pipelines
├── labeling/       # Horizon labels, event windows, target creation
├── analysis/       # Correlation, lead/lag, event studies
├── backtest/       # Signal simulation and evaluation
├── reports/        # Console / markdown / JSON rendering
├── storage/        # SQLite/Postgres adapters and repositories
└── utils/          # Logging, retry, caching, time helpers
