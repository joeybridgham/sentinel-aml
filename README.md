# Sentinel

**BSA / AML Transaction Monitoring Console**

Sentinel is a working demonstration of how a bank Bank Secrecy Act and anti-money-laundering program monitors customer activity for financial crime. It generates synthetic account data, plants recognized money laundering typologies, and detects them with transparent, rules-based logic that an analyst can read, document, and defend.

**Live demo:** https://joeybridgham.github.io/sentinel-aml/

> All data is synthetic. No real persons, accounts, or institutions are represented. This is a portfolio project, not a compliance tool.

## Why it is built this way

Most "fraud detection" projects train a classifier on a public dataset and report an accuracy score. That is not how AML analysts work, and an examiner could not interrogate a black box. Sentinel takes the opposite approach: every alert traces back to the specific transactions that triggered it and the rule that fired, mirroring the explainability that bank programs and regulators expect.

## Features

- **Overview dashboard** with live operational KPIs and charts for severity, typology, and monitored volume
- **Alert queue** with filtering, sorting, and search, consolidated to one alert per customer with secondary indicators
- **Case-file drawer** for each alert: KYC subject profile, plain-language rationale, a typology-specific chart, the triggering transactions, and disposition controls
- **Disposition workflow**: clear as a false positive with a documented reason, escalate to a case, or generate a FinCEN-style Suspicious Activity Report narrative
- **Customer risk register** with KYC-based risk ratings and expected versus observed activity
- **Sanctions screening** against a synthetic OFAC SDN list using fuzzy name matching, with a live name-screening tool and false-positive resolution
- **Methodology** documenting every detection rule, the risk model, and the alert lifecycle

## Detection rules

| Rule | Typology | Summary |
| --- | --- | --- |
| R1 | Structuring | Repeated cash deposits below the $10,000 CTR threshold |
| R2 | Threshold avoidance | Cash or wire activity clustered in the $9,000 to $9,999 band |
| R3 | Round-dollar activity | Concentration of large exact round-value transfers |
| R4 | Rapid pass-through | Funds received and quickly forwarded to multiple parties |
| R5 | Dormant reactivation | Long inactivity followed by sudden high-value movement |
| R6 | Velocity spike | Weekly volume far above the customer baseline |
| R7 | High-risk geography | Counterparties in FATF-listed jurisdictions |
| R8 | Sanctions match | Fuzzy name match to an OFAC SDN entry |

## How it works

- A seeded generator creates roughly 50 customers and 2,400 transactions over a 90-day window, including benign activity that intentionally trips rules so false-positive handling is part of the demonstration.
- Seven distinct bad-actor scenarios are planted and recovered by the detection engine.
- Findings are consolidated by customer; the highest-scoring finding becomes the headline typology and the rest are recorded as additional indicators.
- Risk scores combine rule weight, transaction value, and customer risk factors, then map to Critical, High, Medium, or Low severity.

## Tech

- Single self-contained `index.html`, no build step and no backend
- Vanilla JavaScript with Chart.js for visualization
- Runs entirely client-side, so it is safe to host as a static page

## Run locally

Open `index.html` in any browser, or serve the folder:

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Disclaimer

Every record is synthetic and randomly generated. "Sentinel", "Atlantic Standard Bank, N.A.", and all sanctions list entries are fictional. The sanctions logic is illustrative and is not connected to the live OFAC SDN list. This project is not affiliated with, endorsed by, or representative of any financial institution or government agency, and it is not a compliance tool.

## Author

Built by **Joseph Bridgham**, MS in Finance and Investment Management, University of North Carolina Wilmington.

Portfolio: https://joeybridgham.github.io
