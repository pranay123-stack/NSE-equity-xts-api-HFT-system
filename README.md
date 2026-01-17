# NSE Equity XTS API HFT System

[![C++](https://img.shields.io/badge/C++-20-00599C?style=flat&logo=cplusplus&logoColor=white)](https://isocpp.org/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![XTS](https://img.shields.io/badge/XTS-Symphony-00A86B?style=flat)](https://symphonyfintech.com/)
[![NSE](https://img.shields.io/badge/NSE-Equity-FF6600?style=flat)](https://www.nseindia.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

High-frequency trading system for NSE Cash Market (Equity) using Symphony XTS API with institutional-grade latency and throughput.

---

## Overview

| Metric | Target |
|--------|--------|
| **Latency** | < 100 microseconds |
| **Throughput** | 5,000+ orders/sec |
| **API** | Symphony XTS (IIFL, 5Paisa, etc.) |
| **Instruments** | NIFTY 50, Large & Mid caps |

---

## Features

- **XTS API Integration** - Native Symphony Fintech XTS connectivity
- **Low Latency** - Optimized C++ core with Python strategy layer
- **Multi-Broker** - Works with IIFL, 5Paisa, and other XTS brokers
- **Market Data** - Real-time tick data and order book depth
- **Smart Execution** - Slice orders, iceberg, bracket orders
- **Statistical Arbitrage** - Pairs trading, index arbitrage
- **Co-location Support** - Optimized for broker co-lo environments

---

## XTS API Features

| Feature | Description |
|---------|-------------|
| **Interactive API** | Order placement, modification, cancellation |
| **Market Data API** | Real-time quotes, depth, OHLC |
| **WebSocket** | Streaming market data |
| **Historical Data** | OHLC candles for backtesting |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      NSE EQUITY XTS HFT SYSTEM                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                        XTS API LAYER                                   │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                   │ │
│  │  │ Interactive │  │  Market     │  │  WebSocket  │                   │ │
│  │  │    API      │  │  Data API   │  │   Stream    │                   │ │
│  │  │  (Orders)   │  │  (Quotes)   │  │  (Real-time)│                   │ │
│  │  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘                   │ │
│  │         └────────────────┴────────┬───────┘                          │ │
│  └──────────────────────────────────┬┴──────────────────────────────────┘ │
│                                     ▼                                      │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                         CORE ENGINE                                    │ │
│  │                                                                        │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │ │
│  │  │   Message    │  │   Order      │  │   Position   │                │ │
│  │  │   Parser     │  │   Manager    │  │   Tracker    │                │ │
│  │  │  (C++ Core)  │  │              │  │              │                │ │
│  │  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘                │ │
│  │         └─────────────────┴─────────────────┘                        │ │
│  │                           │                                           │ │
│  │  ┌────────────────────────▼───────────────────────────────────────┐  │ │
│  │  │                   STRATEGY LAYER (Python)                       │  │ │
│  │  │  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌──────────┐ │  │ │
│  │  │  │   Market   │  │   Stat     │  │   Index    │  │  Pairs   │ │  │ │
│  │  │  │   Making   │  │    Arb     │  │    Arb     │  │ Trading  │ │  │ │
│  │  │  └────────────┘  └────────────┘  └────────────┘  └──────────┘ │  │ │
│  │  └────────────────────────────────────────────────────────────────┘  │ │
│  └──────────────────────────────────┬───────────────────────────────────┘ │
│                                     ▼                                      │
│  ┌───────────────────────────────────────────────────────────────────────┐ │
│  │                          RISK LAYER                                    │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │ │
│  │  │  Pre-Trade   │  │   Exposure   │  │    Kill      │                │ │
│  │  │  Validation  │  │   Monitor    │  │   Switch     │                │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘                │ │
│  └───────────────────────────────────────────────────────────────────────┘ │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Strategies

| Strategy | Description | Holding Period |
|----------|-------------|----------------|
| **Market Making** | Two-sided quoting for liquid stocks | Seconds |
| **Statistical Arbitrage** | Mean reversion on correlated pairs | Minutes-Hours |
| **Index Arbitrage** | NIFTY vs NIFTYBEES mispricing | Seconds-Minutes |
| **Momentum Scalping** | Ride short-term momentum | Seconds-Minutes |
| **Event Arbitrage** | Corporate action arbitrage | Event-dependent |

---

## Project Structure

```
NSE-equity-xts-api-HFT-system/
│
├── src/
│   ├── core/                      # C++ Core
│   │   ├── xts_client.hpp
│   │   ├── message_parser.hpp
│   │   ├── order_manager.hpp
│   │   └── utils/
│   │
│   ├── api/                       # XTS API Wrapper
│   │   ├── interactive.py
│   │   ├── marketdata.py
│   │   └── websocket.py
│   │
│   ├── strategy/
│   │   ├── base_strategy.py
│   │   ├── market_making.py
│   │   ├── stat_arb.py
│   │   ├── index_arb.py
│   │   └── pairs_trading.py
│   │
│   ├── risk/
│   │   ├── pre_trade.py
│   │   ├── exposure.py
│   │   └── kill_switch.py
│   │
│   └── utils/
│       ├── config.py
│       └── logger.py
│
├── config/
│   └── config.yaml
│
├── tests/
├── CMakeLists.txt
├── requirements.txt
└── README.md
```

---

## Quick Start

```bash
# Clone repository
git clone https://github.com/pranay123-stack/NSE-equity-xts-api-HFT-system.git
cd NSE-equity-xts-api-HFT-system

# Install Python dependencies
pip install -r requirements.txt

# Build C++ core (optional)
mkdir build && cd build
cmake .. && make -j$(nproc)

# Configure XTS credentials
cp config/config.example.yaml config/config.yaml

# Run
python -m src.main --strategy stat_arb --mode paper
```

---

## Configuration

```yaml
# config/config.yaml
xts:
  broker: IIFL
  api_key: ${XTS_API_KEY}
  api_secret: ${XTS_API_SECRET}
  source: WEBAPI

market_data:
  instruments:
    - RELIANCE
    - TCS
    - HDFCBANK
    - INFY
  depth_level: 5

trading:
  segment: NSECM
  product_type: NRML
  order_type: LIMIT

strategy:
  name: stat_arb
  params:
    pairs:
      - [HDFCBANK, ICICIBANK]
      - [TCS, INFY]
    z_score_entry: 2.0
    z_score_exit: 0.5

risk:
  max_order_value: 2000000
  max_position_value: 10000000
  daily_loss_limit: 50000
```

---

## XTS Broker Setup

1. Open account with XTS-supported broker (IIFL, 5Paisa, etc.)
2. Apply for API access
3. Get API credentials
4. Configure in config.yaml

---

## Coming Soon

- [ ] XTS API integration
- [ ] C++ message parser
- [ ] Market making strategy
- [ ] Statistical arbitrage
- [ ] Index arbitrage
- [ ] Risk management

---

## Risk Warning

**HFT and equity trading involves risk.** Requires significant capital, infrastructure, and expertise. Market conditions can change rapidly. Only for qualified participants.

---

## License

MIT License

---

## Contact

**Pranay** - HFT Developer

[![GitHub](https://img.shields.io/badge/GitHub-pranay123--stack-181717?style=flat&logo=github)](https://github.com/pranay123-stack)
