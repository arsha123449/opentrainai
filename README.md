# OpenTrainAI ($OTAI)

OpenTrainAI is a decentralized Layer-1 Proof-of-Useful-Work (PoUW) blockchain network designed to monetize GPU compute power by replacing traditional, wasteful hashing algorithms with real-world AI micro-task execution (inference, fine-tuning, embeddings).

Nodes earn native `$OTAI` coins based on task completion time, compute difficulty, and network uptime.

---

## 🚀 Core Features

* **Proof-of-Useful-Work (PoUW) Consensus:** Native Layer-1 mining driven by executing AI workloads (PyTorch, LoRA, QLoRA, embeddings) rather than arbitrary math puzzles.
* **Execution & Time-Based Rewards:** Dynamic emissions based on verified task duration and compute difficulty ratings.
* **Hardcoded Protocol Fee Routing:** Built-in protocol-level ledger split distributing rewards automatically on every mined block.
* **3-Year Halving Schedule:** Fixed supply decay curve halving emissions every 3,155,760 blocks to manage inflation and promote long-term token scarcity.

---

## 💰 Network Economics ($OTAI)

* **Token Ticker:** `$OTAI`
* **Total Max Supply:** `110,000,000,000` (110 Billion Native Coins)
* **Block Time:** `30 seconds`
* **Halving Interval:** `3,155,760 blocks` (~3 Years)

### Supply Allocation

| Pool | Allocation (%) | Total Tokens | Purpose |
| :--- | :--- | :--- | :--- |
| **Mining & Compute Rewards** | 97.0% | 106,700,000,000 $OTAI | Distributed to native GPU miner nodes via PoUW |
| **Development Treasury** | 2.0% | 2,200,000,000 $OTAI | Protocol development, RPC node hosting, & network grants |
| **Founders Allocation** | 1.0% | 1,100,000,000 $OTAI | Core protocol founders & early team reserve |

### Protocol Payout Split

Every newly mined block automatically routes block rewards on the ledger level:
* **97%** $\rightarrow$ Winning Miner Node (GPU Worker)
* **2%** $\rightarrow$ Development Treasury Wallet
* **1%** $\rightarrow$ Founders Wallet

---

## ⛏️ Halving Schedule & Emission Lifespan

With a 30-second block time and 3-year halving intervals, ~93.7% of all coins are mined within the first 12 years. The total supply is asymptotically approached over 30+ years before mining transitions strictly to network transaction fees.

| Era | Timeline | Block Height Range | Base Block Reward | Worker (97%) | Dev Treasury (2%) | Founder (1%) | Cumulative Supply Mined |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Era 1** | Years 1–3 | `0` – `3,155,759` | **16,905.50 $OTAI** | 16,398.33 $OTAI | 338.11 $OTAI | 169.06 $OTAI | 50.00% (53.35B) |
| **Era 2** | Years 4–6 | `3,155,760` – `6,311,519` | **8,452.75 $OTAI** | 8,199.17 $OTAI | 169.05 $OTAI | 84.53 $OTAI | 75.00% (80.02B) |
| **Era 3** | Years 7–9 | `6,311,520` – `9,467,279` | **4,226.37 $OTAI** | 4,099.58 $OTAI | 84.53 $OTAI | 42.26 $OTAI | 87.50% (93.36B) |
| **Era 4** | Years 10–12 | `9,467,280` – `12,623,039` | **2,113.18 $OTAI** | 2,049.79 $OTAI | 42.26 $OTAI | 21.13 $OTAI | 93.75% (100.03B) |
| **Era 5** | Years 13–15 | `12,623,040` – `15,778,799` | **1,056.59 $OTAI** | 1,024.89 $OTAI | 21.13 $OTAI | 10.57 $OTAI | 96.87% (103.36B) |

---

## 🛠 Tech Stack

* **Layer-1 Node & Consensus Engine:** C++ / Rust / Go (`libp2p`, RocksDB state ledger, JSON-RPC API)
* **Worker Execution Client:** Python (PyTorch, Hugging Face `transformers`, `peft` / LoRA, vLLM)
* **Wallet & Client Infrastructure:** Native CLI Wallet (`opentrain-cli`), REST / WebSocket RPC API

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
