# Exchange Finder Matrix & Execution Benchmarking Model

An open-source data schema and matching logic blueprint to evaluate crypto exchanges across execution speed, maker/taker fee tiers, and jurisdictional compliance.

Powered by the research engine at [ExchangeCatalogue](https://exchangecatalogue.com/).

---

## Live Web Implementation
To test the interactive production implementation with live exchange data feeds, access the web selector directly:
* **[Launch the Interactive Exchange Finder](https://exchangecatalogue.com/tools/exchange-finder/)**

---

## Matrix Evaluation Criteria
The matrix scores trading venues across four operational vectors:

| Scoring Vector | Key Metrics Evaluated | Weighting |
| :--- | :--- | :--- |
| **API Connectivity** | WebSocket streaming latency, REST throughput limits, sub-account routing | 30% |
| **Liquidity & Slippage** | 2% market depth on major pairs (BTC/ETH), order book thickness | 30% |
| **Fee Economics** | VIP maker/taker tiers, withdrawal fees, funding rates | 25% |
| **Security & Custody** | Proof of reserves (PoR), multi-signature isolation, license coverage | 15% |

---

## Sample Evaluation Snippet (Python)
```python
def score_exchange_viability(maker_fee, api_ping_ms, depth_score):
    """
    Computes a simplified execution efficiency score (0-100 scale).
    """
    fee_penalty = maker_fee * 1000
    latency_penalty = max(0, (api_ping_ms - 50) * 0.2)
    composite_score = (depth_score * 0.6) - fee_penalty - latency_penalty
    return round(max(0, composite_score), 2)

# Benchmark example
print("Venue Score:", score_exchange_viability(maker_fee=0.0002, api_ping_ms=42, depth_score=95))
