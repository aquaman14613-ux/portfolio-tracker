# St0ck v1.2 — Rules Reference for Automated Reports

## Source tiers (for news items)
A-primary (SEC/filings), B-institutional (FactSet/LSEG), C-independent analysis (Morningstar), D-news (Reuters-caliber), E-alternative signals (insider/politician), F-sentiment (social media)

## Thresholds
- Single-position ceiling: 10% (12% = mandatory review)
- Theme/sector correlation cap: 30% (same GICS sub-industry, OR >0.7 trailing 12mo correlation, OR shared single revenue driver)
- Cash target: 7.5–10%
- Price review triggers: -15% from cost (formal review), -20% (documented decision required)
- Shariah: current Zoya compliance is a hard pass/fail gate

## Concentration check exclusions
SPUS is a diversified Shariah-compliant benchmark ETF, not a single-stock concentration risk. Exclude it entirely from the 10%/12% single-position ceiling check. It should never trigger a concentration alert regardless of its weight.

## Data hygiene
If IBKR reports a position with 0 shares (fully closed), exclude it entirely from position tables and P&L reporting — do not surface phantom/residual entries from closed positions.

## Report tone
Concise, tabular where useful, no repeated caveats, no restating these rules in output — just apply them.

## Fallback behavior (if IBKR is unreachable)
Read last_snapshot.json in this repo. State: "Portfolio data last confirmed [timestamp] — IBKR temporarily unreachable, using last known positions." Web-search current prices for held tickers for context.

## Search budget
Max 1 search per ticker needing news. Combine tickers into one query where possible before falling back to individual searches. Cap total searches per run at a reasonable number — don't over-search on ambiguous results.

## Alert dedup
Before sending any concentration or price-threshold alert, check today_alerts.json first. Only send if this is a genuinely new breach not already logged today. Always write the new alert to today_alerts.json immediately after sending, before ending the run.

## Schedule discipline
Hourly checks should only run during market hours on weekdays. If triggered outside that window (e.g. weekend), end immediately with no report and no alert.
