# Polymarket Trade Monitor

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

Real-time monitor for large trades on Polymarket with beautiful terminal UI, keyword filtering, and anomaly detection.

## Features

- **Interactive Setup Wizard** - Easy first-time configuration
- **Beautiful Terminal UI** - Colored output with panels and tables
- **Large Trade Monitoring** - Track trades above a configurable threshold
- **Keyword/Topic Filtering** - Monitor only trades matching specific topics
- **Anomaly Detection** - Flag suspicious low-price + high-size trades
- **Wallet/Username Tracking** - Monitor specific traders
- **Discord Notifications** - Get alerts for anomalous trades
- **CSV Export** - All trades saved with full details

## Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/polymarket-monitor.git
cd polymarket-monitor

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the monitor
python monitor.py
```

On first run, an interactive setup wizard will guide you through configuration.

## Setup Wizard

When you run the monitor for the first time (or with `--setup`), you'll be guided through:

1. **Discord Webhook** (optional) - For receiving trade notifications
2. **Minimum Trade Amount** - Only monitor trades above this USD value
3. **Anomaly Criteria** - Configure what makes a trade "suspicious"
4. **Trade Age Filter** - Ignore old trades
5. **Keyword Filtering** - Filter by market topics (e.g., bitcoin, politics, sports)

All settings are saved to `.env` and loaded automatically on next run.

## Keyword Filtering

Filter trades by topic/theme to focus on markets you care about.

### Configuration

```env
# Single topic
KEYWORDS=bitcoin

# Multiple topics (comma-separated)
KEYWORDS=bitcoin,ethereum,crypto

# Match mode
KEYWORD_MATCH_MODE=any   # Show trades matching ANY keyword (default)
KEYWORD_MATCH_MODE=all   # Show only trades matching ALL keywords
```

### Examples

| Keywords | Match Mode | Matches |
|----------|------------|---------|
| `bitcoin,ethereum` | any | "Will Bitcoin hit $100k?" or "Ethereum price prediction" |
| `trump,election` | any | "Trump wins 2024?" or "Election day results" |
| `nba,championship` | all | Only "NBA Championship winner" (must contain both) |

Leave `KEYWORDS` empty to show all trades (no filtering).

## Operating Modes

### Mode 1: Large Trade Monitor
Monitors all trades above the configured minimum amount. Discord notifications are sent only for anomalous trades.

### Mode 2: Wallet/Username Tracking
Track specific traders by:
- **Wallet address** (0x...)
- **Polymarket username**

All trades from tracked identities are shown, regardless of amount.

## Configuration

Configuration is stored in `.env`. You can edit it manually or run `python monitor.py --setup`:

```env
# Discord webhook URL for notifications (optional)
DISCORD_WEBHOOK=https://discord.com/api/webhooks/...

# Minimum trade amount to monitor (USD)
MIN_TRADE_AMOUNT=1000

# Anomaly detection criteria
ANOMALY_PRICE_MAX=0.4
ANOMALY_SIZE_MIN=10000
ANOMALY_AMOUNT_MIN=500

# Maximum age of trades to consider (minutes)
MAX_TRADE_AGE_MINUTES=30

# Keyword filtering
KEYWORDS=bitcoin,crypto
KEYWORD_MATCH_MODE=any

# Check interval (seconds)
LOOP_INTERVAL=1
```

## Anomaly Detection

A trade is flagged as **anomalous** when ALL of these conditions are met:
- Price <= `ANOMALY_PRICE_MAX` (default: 0.4)
- Size >= `ANOMALY_SIZE_MIN` (default: 10,000)
- Amount >= `ANOMALY_AMOUNT_MIN` (default: $500)

This helps identify potentially significant bets at low prices.

## Output Files

| File | Description |
|------|-------------|
| `large_trades.csv` | Log of all detected trades with timestamps |
| `tracked_wallets.txt` | Saved wallet addresses for tracking mode |
| `tracked_usernames.txt` | Saved usernames for tracking mode |

## Example Output

```
+==================================+
|   POLYMARKET TRADE MONITOR       |
+==================================+

+------------------+----------------------+
| Setting          | Value                |
+------------------+----------------------+
| Mode             | Large Trade Monitor  |
| Min Amount       | $1,000               |
| Anomaly          | price<=0.4, size>=10000 |
| Keywords         | bitcoin, crypto      |
| Match Mode       | any                  |
| Discord          | Configured           |
+------------------+----------------------+

Received 100 trades >= $1,000

+-------- Trade --------+
| Hash    | 0x8c448b... |
| Amount  | $5,250.00   |
| Price   | 0.3500      |
| Size    | 15,000.00   |
| Market  | Will BTC... |
| Keywords| bitcoin     |
+-----------------------+

Processed 3 new trade(s)
```

## Requirements

- Python 3.10+
- Dependencies: `requests`, `python-dotenv`, `rich`

## License

MIT License - feel free to use and modify.

## Contributing

Pull requests are welcome! For major changes, please open an issue first.
