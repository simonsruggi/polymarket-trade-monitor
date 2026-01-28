# Polymarket Monitor

Python script to monitor prediction markets on Polymarket and track large trades in real-time.

## Tech Stack

- **Language**: Python 3.10+
- **Main Libraries**:
  - requests (HTTP requests)
  - python-dotenv (environment configuration)
  - rich (terminal UI with colors, tables, panels)

## Important Files/Folders

- `monitor.py` - Main monitoring script
- `requirements.txt` - Python dependencies
- `.env` - Configuration file (created by setup wizard)
- `.env.example` - Example configuration
- `large_trades.csv` - Log of detected trades (auto-generated)
- `tracked_wallets.txt` - Wallet addresses for tracking mode
- `tracked_usernames.txt` - Usernames for tracking mode

## Useful Commands

```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Run monitor (first run will start setup wizard)
python monitor.py

# Run setup wizard again
python monitor.py --setup
```

## Features

- Interactive setup wizard on first run
- Beautiful colored terminal output using Rich library
- Two modes: Large trade monitor and Wallet/Username tracking
- Anomaly detection for suspicious trades
- Discord webhook notifications
- CSV export of all trades

## Configuration

All settings are stored in `.env` file:
- `DISCORD_WEBHOOK` - Discord webhook URL for notifications
- `MIN_TRADE_AMOUNT` - Minimum USD amount to monitor
- `ANOMALY_PRICE_MAX` - Maximum price to flag as anomaly
- `ANOMALY_SIZE_MIN` - Minimum size to flag as anomaly
- `MAX_TRADE_AGE_MINUTES` - Ignore trades older than this
