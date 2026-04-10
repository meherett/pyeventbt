# Changelog

All notable changes to PyEventBT will be documented in this file.

## [0.0.7] - 2026-04-10

### Features
- Added CHANGELOG.md with automated GitHub release notes extraction from the changelog on each release.

### Bug Fixes
- Fixed multi-symbol equity calculation in backtesting simulator. Equity now accounts for floating PnL across all open positions (all symbols), matching live MT5 behavior. Previously, equity only reflected the PnL of the symbol whose bar was being processed, causing incorrect equity, free margin, and margin call checks in multi-symbol strategies.
- Replaced mutable default arguments in Strategy method signatures (`custom_signal_engine`, `configure_predefined_signal_engine`, `backtest`, `run_live`) with `None` defaults to prevent potential shared-state bugs across multiple calls.
- Consolidated FX symbol list into a single `ALL_FX_SYMBOLS` constant in `utils.py`, replacing 4 duplicated tuples across the execution engine connector, sizing engine, and utils. Added missing `USDMXN` and `EURMXN` pairs to the connector and sizing engine, which previously applied incorrect CFD margin/commission formulas for those pairs.
- Fixed logger name in `utils.py` from `"PyEventBT"` to `"pyeventbt"` so log messages from utility functions are captured by the framework's logger handlers.
- Replaced bare `IndexError` in currency conversion lookups (`utils.py`, `mt5_risk_pct_sizing.py`) with a descriptive `ValueError` indicating the unsupported currency pair and how to resolve it.
- Added `SharedData` reset at the start of each backtest to prevent simulator state (symbol info, account info, error codes) from leaking between sequential backtest runs (e.g. optimization loops).

## [0.0.6] - 2026-03-15

### Features
- Added TRIX, DeMarker and RVI indicators (@kevin-bruton)
- Updated README examples (@kevin-bruton)

### Bug Fixes
- Fixed strategy_id in Quantdle MA crossover example (@kevin-bruton)
- Fixed example strategies (@kevin-bruton)

## [0.0.5] - 2026-03-10

### Features
- Added CSV export for backtest results
- Pointed homepage to dedicated website (pyeventbt.com)

### Bug Fixes
- Ensured precision in MT5 sizing calculations
- Fixed README example syntax

## [0.0.4] - 2025-12-06

### Bug Fixes
- Handled MT5 import errors gracefully for non-Windows platforms

## [0.0.3] - 2025-12-06

### Features
- Added CLI application with `info` command
- Read version from package metadata

## [0.0.2] - 2025-12-06

### Features
- Initial full framework release with all core modules:
  - Event-driven backtesting and live trading engine
  - MT5 simulator wrapper and broker connectors
  - Data provider with CSV backtesting and MT5 live data support
  - Signal, sizing, and risk engine services with predefined and custom implementations
  - Portfolio and position management
  - Trade archiver and execution engine
  - Technical indicators (ATR, SMA, EMA, KAMA)
  - Hook service, schedule service, and trading context management
  - Strategy class with decorator-based API
  - Example strategies (MA crossover, Bollinger Bands breakout, Quantdle MA crossover)

## [0.0.1] - 2025-10-08

### Features
- Initial project structure, CI workflow, and Poetry configuration

# Changelog Format

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
