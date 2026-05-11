# trade-v1-seed

Auto-published level CSVs for TradingView `request.seed()` consumption.

This repo is the public delivery channel for the
[trade-v1](https://github.com/Aamirk11/trade-v1) technical-analysis engine.
A GitHub Action in the private trade-v1 repo runs every hour and pushes
freshly-computed levels (S/R zones, volume profile, anchored VWAPs,
liquidation magnets) here, formatted as OHLCV CSVs.

The Pine v6 indicator at `pine/scratch/claude-scratch-native-*.pine` in
the trade-v1 repo reads from these CSVs via `request.seed("Aamirk11/trade-v1-seed", TICKER)`.

## Feed encoding

Each TICKER follows `{SYMBOL}_{TF}_{FEED}` (e.g. `BTCUSDT_1H_VP`).

| Feed | O | H | L | C | V |
|---|---|---|---|---|---|
| VP    | POC R7d  | VAH R7d  | VAL R7d  | POC PD     | POC PW       |
| RES   | R1       | R2       | R3       | R4         | R5           |
| SUP   | S1       | S2       | S3       | S4         | S5           |
| AVWAP | session  | weekly   | monthly  | swing-high | swing-low    |
| LIQ   | long-near| short-near| long-big| short-big  | density (M$) |

## Update cadence

Hourly via GitHub Actions cron (top-of-hour, drifts 5–15 min on GitHub-hosted runners).

Do not commit by hand — the workflow is the source of truth.
