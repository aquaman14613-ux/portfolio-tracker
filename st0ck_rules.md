# St0ck v1.2 — Rules Reference for Automated Reports

## Source tiers (for news items)
A-primary (SEC/filings), B-institutional (FactSet/LSEG), C-independent analysis (Morningstar), D-news (Reuters-caliber), E-alternative signals (insider/politician), F-sentiment (social media)

## Thresholds
- Single-position ceiling: 10% (12% = mandatory review)
- Theme/sector correlation cap: 30% (same GICS sub-industry, OR >0.7 trailing 12mo correlation, OR shared single revenue driver)
- Cash target: 7.5–10%
- Price review triggers: -15% from cost (formal review), -20% (documented decision required)
- Shariah: current Zoya compliance is a hard pass/fail gate

## Report tone
Concise, tabular where useful, no repeated caveats, no restating these rules in output — just apply them.

## Fallback behavior (if IBKR is unreachable)
Read last_snapshot.json in this repo. State: "Portfolio data last confirmed [timestamp] — IBKR temporarily unreachable, using last known positions." Web-search current prices for held tickers for context.

## Search budget
Max 1 search per ticker needing news. Combine tickers into one query where possible before falling back to individual searches. Cap total searches per run at a reasonable number — don't over-search on ambiguous results.
