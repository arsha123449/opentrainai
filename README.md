# OpenTrainAI ($OTAI)

OpenTrainAI is a decentralized Layer-1 Proof-of-Useful-Work (PoUW) blockchain network designed to monetize consumer and enterprise GPU compute power. Instead of wasting energy on arbitrary hashing algorithms, OpenTrainAI node operators earn native `$OTAI` coins by executing real-world AI micro-tasks including inference, parameter-efficient fine-tuning (LoRA/QLoRA), and embedding generation.

---

## 🚀 Core Features

* **Proof-of-Useful-Work (PoUW) Consensus:** Native Layer-1 consensus where block proposal rights and rewards are earned through verified AI workload execution using PyTorch, vLLM, and Hugging Face libraries.
* **Score-Based Dynamic Emissions:** Block rewards are distributed based on verified task duration, difficulty ratings, and GPU benchmark performance.
* **Hardcoded Protocol Fee Routing:** Automated on-chain ledger logic that distributes minted block rewards directly across workers, development treasury, and founders.
* **3-Year Halving Schedule:** Programmatic emission halving every 3,155,760 blocks to enforce long-term scarcity and manage supply inflation over a 30+ year timeline.

---

## 💰 Network Economics ($OTAI)

* **Token Ticker:** `$OTAI`
* **Total Max Supply:** `110,000,000,000` (110 Billion Native Coins)
* **Block Time Interval:** `30 seconds`
* **Halving Interval:** `3,155,760 blocks` (~3 Years)

### Supply Allocation

| Pool | Allocation (%) | Total Tokens | Purpose |
| :--- | :--- | :--- | :--- |
| **Mining & Compute Rewards** | 97.0% | 106,700,000,000 $OTAI | Distributed to active GPU worker nodes executing PoUW |
| **Development Treasury** | 2.0% | 2,200,000,000 $OTAI | Core protocol dev, validator infrastructure, and grants |
| **Founders Allocation** | 1.0% | 1,100,000,000 $OTAI | Founding team reserve |

### Protocol Reward Split

On every newly accepted block, the consensus engine split distributes the block's emission on the native ledger level:
* **97%** $\rightarrow$ Active GPU Worker Nodes
* **2%** $\rightarrow$ Development Treasury Wallet
* **1%** $\rightarrow$ Founders Wallet

---

## ⚙️ How the Network Works

### 1. Task Submission & P2P Routing
Developers and users submit AI tasks (e.g., fine-tuning a 7B model micro-batch) along with network fees in `$OTAI`. Tasks enter the network mempool and are routed to active worker nodes based on GPU VRAM availability and network latency.

### 2. Distributed AI Training & Execution
Workers load the target model weights and execute forward/backward passes locally:
* **LoRA/QLoRA Fine-Tuning:** Workers update low-rank adapter matrices ($\Delta w$) rather than full model weights, keeping bandwidth requirements low.
* **Execution Logging:** Workers record compute execution time ($T_{\text{executed}}$) using high-resolution CUDA hardware timers (`cudaEventElapsedTime`).

### 3. Verification & Fraud Prevention
Before work is accepted, workers broadcast their LoRA weight deltas ($\Delta w$), output loss values, and execution metrics to the network:
* **Redundant Verification:** The orchestrator assigns the same micro-task payload to $N$ random verifier nodes.
* **Consensus Check:** Verifier nodes perform sample passes. If the submitted loss and output gradients match verifier consensus, the worker submission is marked as valid ($R_{\text{verifier}} = 1.0$). If fraud is detected, $R_{\text{verifier}} = 0.0$ and the node receives zero payout.

### 4. Federated Aggregation
Once verified, the network aggregates individual worker LoRA updates using **Federated Averaging (FedAvg)** to update the global model state for subsequent task batches:

$$\text{Global Weight}_{t+1} = \text{Global Weight}_t + \eta \sum_{i=1}^{N} \Delta w_i$$

---

## 📊 Compute Score & Reward Formula

When a 30-second block window closes, the consensus engine calculates a **Compute Score ($S$)** for every worker with verified completed tasks:

$$S = \text{Task Difficulty } (D) \times \text{Execution Duration } (T_{\text{executed}}) \times \text{Hardware Multiplier } (M_{\text{hardware}}) \times R_{\text{verifier}}$$

### Reward Distribution Formula

Each worker's payout from the block's **97% Worker Pool** is determined by their proportional score share relative to all active workers in that block:

$$\text{Worker Reward} = \left( \frac{S_{\text{worker}}}{\sum S_{\text{all workers in block}}} \right) \times \left( R_{\text{block}} \times 0.97 \right)$$

* **$S_{\text{worker}}$:** Your node's total compute score earned in the 30-second block window.
* **$\sum S_{\text{all workers in block}}$:** The sum of all compute scores across every valid node in the network for that block.
* **$R_{\text{block}}$:** The native base block reward ($16,905.50\ \text{OTAI}$ in Era 1).

---

## ⛏️ Halving Schedule & Emission Lifespan

With 30-second block times and 3-year halving intervals, ~93.7% of all coins are mined within the first 12 years. Supply cap limits are enforced at the protocol consensus layer.

| Era | Timeline | Block Height Range | Base Block Reward | Worker Pool (97%) | Dev Treasury (2%) | Founder Fee (1%) | Cumulative Supply Mined |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Era 1** | Years 1–3 | `0` – `3,155,759` | **16,905.50 $OTAI** | 16,398.33 $OTAI | 338.11 $OTAI | 169.06 $OTAI | 50.00% (53.35B) |
| **Era 2** | Years 4–6 | `3,155,760` – `6,311,519` | **8,452.75 $OTAI** | 8,199.17 $OTAI | 169.05 $OTAI | 84.53 $OTAI | 75.00% (80.02B) |
| **Era 3** | Years 7–9 | `6,311,520` – `9,467,279` | **4,226.37 $OTAI** | 4,099.58 $OTAI | 84.53 $OTAI | 42.26 $OTAI | 87.50% (93.36B) |
| **Era 4** | Years 10–12 | `9,467,280` – `12,623,039` | **2,113.18 $OTAI** | 2,049.79 $OTAI | 42.26 $OTAI | 21.13 $OTAI | 93.75% (100.03B) |
| **Era 5** | Years 13–15 | `12,623,040` – `15,778,799` | **1,056.59 $OTAI** | 1,024.89 $OTAI | 21.13 $OTAI | 10.57 $OTAI | 96.87% (103.36B) |

---

## 🛠 Tech Stack

* **Layer-1 Node & Consensus Engine:** Rust / C++ / Go (`libp2p`, RocksDB state ledger, JSON-RPC API)
* **Worker Execution Client:** Python (`PyTorch`, `huggingface/transformers`, `peft` / LoRA, `vLLM`, `pynvml`)
* **Client & Tooling:** Native CLI Wallet (`opentrain-cli`), REST / WebSocket RPC endpoints

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
