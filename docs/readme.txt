# Sentinel 2.0: Multi-Platform Social Sentiment & Market Signal Lab

Sentinel 2.0 is a research-grade, command-line platform for collecting social discussion data,
extracting finance-aware signals, and evaluating whether those signals have predictive value
for stocks and cryptocurrencies across multiple time horizons.

Unlike a single “sentiment vs price correlation” script, Sentinel 2.0 is built as a reproducible
pipeline:
  1) ingest raw events (immutable)
  2) normalize + detect symbols/entities
  3) compute features (versioned)
  4) run analyses + backtests (out-of-sample)
  5) produce explainable reports

## Project goals

- Make social sentiment analysis *testable and reproducible* (data versioning + pipelines).
- Support realistic evaluation: out-of-sample splits, multiple horizons, and robustness checks.
- Provide explainable outputs: “what changed, where, and when” — not just a score.
- Remain “batteries included” for local research, but scale to Postgres/Redis/Docker when needed.

## Core capabilities

Data sources (connectors)
- Reddit: subreddit and keyword-based collection (posts + comments) with incremental backfills.
- X (Twitter): keyword/symbol queries and near-real-time collection, depending on your access level.
- Optional: Google Trends attention proxy connector.
- Optional: StockTwits sentiment connector (enterprise access may be required).

Finance-aware NLP
- Fast baseline sentiment scoring (lexicon/rule-based).
- Finance-domain sentiment scoring (FinBERT-style transformer models).
- Metadata features: emoji/negation emphasis, “certainty” markers, question vs assertion, etc.
- Topic & narrative clustering (embeddings) so reports can summarize what the crowd is talking about.

Entity & symbol extraction
- Robust ticker extraction with disambiguation rules (supports $TSLA, “TSLA”, and common formats).
- Instrument master (stocks/ETFs/crypto) to validate candidates and reduce false positives.
- Multi-symbol attribution (one post mentioning multiple tickers is handled explicitly).

Feature engineering
- Attention: mention volume, unique authors, engagement-weighted volume, burstiness, decay.
- Sentiment: mean, distribution, extremes, disagreement between scoring engines.
- Conversation structure: replies depth, cross-posts, repeating text, duplicated content rate.
- Market context: returns/volatility/volume features and “abnormal activity” baselines.

Analysis & backtesting
- Correlation + lead/lag analysis at multiple lags and horizons.
- Event studies: “what happens after a sentiment spike?”
- Predictive tests: simple baselines first (linear/logistic), then optional ML models.
- Strategy backtests (optional): supports transaction-cost assumptions and walk-forward evaluation.

Reporting
- Rich CLI outputs (tables + charts) and exportable reports (HTML/Markdown/JSON).
- “Signal cards” per asset: key drivers, horizon where signal appears, stability across time splits.

## Non-goals

- Sentinel is not a broker, execution engine, or real-money trading system.
- Sentinel does not claim to identify “the” reason a price moved.
- Sentinel is built for research workflows: evaluate signals, iterate safely, and measure robustness.

## Tech stack

Language
- Python 3.11+

Core libraries
- Data: pandas, numpy
- NLP: vaderSentiment, transformers (optional), sentence-transformers (optional)
- Time series / stats: statsmodels, scipy
- CLI/UI: typer, rich
- Storage: SQLite (default), PostgreSQL (recommended for scale)
- Pipeline/orchestration: a lightweight internal runner (upgrade path to Airflow later)

## Repository layout (proposed)

sentinel/
  cli/                   # typer app, commands, output formatting
  connectors/            # reddit, x, trends, stocktwits (optional)
  nlp/                   # sentiment engines, embeddings, text normalization
  instruments/           # symbol master, exchanges, crypto mappings
  features/              # feature computation and versioning
  labeling/              # horizon-based labels and event definitions
  analysis/              # correlations, lead/lag, event study, granger tests
  backtest/              # portfolio simulation + metrics (optional)
  storage/               # DB models, migrations, data access layer
  reports/               # report builders (md/html/json)
  utils/                 # logging, config, rate limiting, retries
tests/

## Installation

### Local dev

1) Clone
    git clone https://github.com/yourusername/sentinel-analysis.git
    cd sentinel-analysis

2) Create and activate venv
    python -m venv venv
    # Windows
    .\venv\Scripts\activate
    # macOS/Linux
    source venv/bin/activate

3) Install
    pip install -r requirements.txt
    pip install -e .

### Optional: GPU / transformer extras
    pip install -r requirements-ml.txt

## Configuration

Create a .env in the project root:

  # Reddit API credentials
  REDDIT_CLIENT_ID=...
  REDDIT_CLIENT_SECRET=...
  REDDIT_USER_AGENT="sentinel/2.0 by yourname"

  # X API credentials (varies by auth style)
  X_BEARER_TOKEN=...

  # Database (optional)
  DATABASE_URL=sqlite:///sentinel.db
  # or
  # DATABASE_URL=postgresql+psycopg://user:pass@localhost:5432/sentinel

  # Feature store / cache (optional)
  REDIS_URL=redis://localhost:6379/0

Add .env to .gitignore immediately.

## Quick start

1) Collect a small dataset (example)
    sentinel collect reddit --subreddit wallstreetbets --query "TSLA" --since 7d
    sentinel collect x --query "TSLA OR $TSLA" --since 7d

2) Build features
    sentinel features build --symbol TSLA --timeframe 15m --lookback 30d

3) Run analysis
    sentinel analyze --symbol TSLA --horizons 1h 4h 1d 3d 7d --report html

4) View report output
    open ./reports/TSLA/latest/index.html

## CLI commands (planned)

Data ingestion
- sentinel collect reddit ...
- sentinel collect x ...
- sentinel backfill --symbol TSLA --days 365

Data processing
- sentinel normalize --source reddit --since 30d
- sentinel features build --symbol TSLA --timeframe 15m --lookback 180d

Research & evaluation
- sentinel analyze --symbol TSLA --horizons ...
- sentinel event-study --symbol TSLA --event sentiment_spike --window -2d +10d
- sentinel granger --x sentiment --y returns --symbol TSLA --lags 1 2 3 5

Backtesting (optional)
- sentinel backtest --signal sentiment_zscore --symbol TSLA --costs 10bps --walk-forward

Maintenance
- sentinel db migrate
- sentinel doctor  # verifies creds, DB, and connector reachability

## Development

Quality gates
- ruff (lint)
- black (format)
- pytest (tests)
- mypy (optional typing)

Run:
    ruff check .
    pytest -q

## Roadmap

Phase 1: Reliable ingestion + storage
- Connectors, caching, rate-limit handling, raw-event schema, SQLite support

Phase 2: Feature store + analysis suite
- Multi-horizon labeling, lead/lag correlations, event studies, report generator

Phase 3: ML experiments + robustness
- Time-aware splits, baseline models, model registry, reproducible experiments

Phase 4: Scaling and product polish
- Postgres + migrations, Docker Compose, CI, scheduled jobs, dashboards

## License

MIT

*This README is a living document and will be updated throughout the project's development.*
