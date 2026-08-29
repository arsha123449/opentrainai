# OpenTrainAI ($OTAI)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Rust](https://img.shields.io/badge/Built%20with-Substrate-orange)](https://substrate.io/)
[![PoUW](https://img.shields.io/badge/Consensus-PoUW-blue)](#)

**OpenTrainAI** is a decentralized **Layer-1 Proof-of-Useful-Work (PoUW)** blockchain network designed to monetize consumer and enterprise GPU compute power. Instead of wasting energy on arbitrary hashing algorithms, node operators earn native `$OTAI` coins by executing real-world AI micro-tasks including inference, parameter-efficient fine-tuning (LoRA/QLoRA), and embedding generation.

Built on the **Substrate framework**, OpenTrainAI operates as a **standalone (solo) chain**. It does not require connection to Polkadot, but can be explored using standard Substrate tools like Polkadot-JS Apps or Statescan.

---

## 🚀 Core Features

- **Proof-of-Useful-Work (PoUW):** Native Layer-1 consensus where block rewards are earned through verified AI workload execution (PyTorch, vLLM, Hugging Face).
- **Hardened Compute Score:** Prevents hardware spoofing and ghost-worker attacks using a multi-variable formula:  
  `ComputeUnits = (HardwareScore × UptimeScore) × JobMultiplier`.
- **Two-Tier Node Architecture:** 
  - **GPU Workers** execute AI tasks (earn 92% of emissions).
  - **Master Nodes (Validators)** produce blocks, track the full chain, and route P2P traffic (earn 5% of emissions).
- **Idle = Zero Mint:** If no GPU workers are active, the 92% (GPU), 2% (Treasury), and 1% (Founders) pools mint **zero**. Only Master Nodes receive their 5% liveness reward to keep the chain producing blocks.
- **Genesis Bootstrapping Bonus:** The first 1,000 active blocks feature a **2x reward multiplier** for GPU Workers, Treasury, and Founders. **Master Nodes are explicitly excluded**, as they were already compensated during the initial idle period.
- **3-Year Halving Schedule:** Programmatic emission halving every 3,155,760 blocks to enforce long-term scarcity.

---

## 💰 Tokenomics & Supply Allocation

**Token Ticker:** `$OTAI`  
**Total Max Supply:** `110,000,000,000` (110 Billion)  
**Block Time:** `30 Seconds`  
**Halving Interval:** `3,155,760 blocks` (~3 Years)

### Final Supply Allocation

| Pool | Allocation | Total Tokens | Minting Mechanism |
| :--- | :--- | :--- | :--- |
| **GPU Mining & Compute Rewards** | 92.0% | 101,200,000,000 | Emitted dynamically via PoUW (Blocks 1+) |
| **Master Node Staking Rewards** | 5.0% | 5,500,000,000 | Emitted per block for validators |
| **Development Treasury** | 2.0% | 2,200,000,000 | Genesis Mint (1.5% Dev + 0.5% Quarterly Buyback) |
| **Founders Allocation** | 1.0% | 1,100,000,000 | Genesis Mint |
| **Total** | **100%** | **110,000,000,000** | |

### Block Reward Split (Era 1)

| Recipient | Percentage | OTAI per Block |
| :--- | :--- | :--- |
| **GPU Worker Pool** (via Compute Score) | **92.0%** | 15,553.06 |
| **Master Node Validators** (Pro-rata by Stake) | **5.0%** | 845.27 |
| **Development Treasury** (Dev + Buyback Vault) | **2.0%** | 338.11 |
| **Founders Allocation** | **1.0%** | 169.06 |
| **Total** | **100%** | **16,905.50** |

---

## ⚙️ Economic Rules & Network States

### 1. The "Idle = Zero Mint" Rule
To prevent the "Zombie Founder" exploit (where teams print money without providing utility):

- **If `active_workers == 0`** (no GPUs mining):
  - The blockchain mints **only the 5% Master Node reward** (`845.27 OTAI`/block).
  - GPU Workers, Treasury, and Founders receive **ZERO** until a GPU worker connects.

- **If `active_workers > 0`** (GPUs are mining):
  - The full `16,905.50 OTAI` reward is minted and distributed per the 92/5/2/1 split.

### 2. The Bootstrapping Bonus (First 1,000 Active Blocks)
When the first GPU workers join the network (triggering Block 1001), a **1,000-block "Bootstrapping Phase"** begins to compensate early adopters for the lost idle period.

| Phase | Blocks | GPU Workers | Master Nodes | Treasury | Founders |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Idle** | 1 – 1000 | **0 OTAI** | 845.27 OTAI | 0 OTAI | 0 OTAI |
| **Bootstrapping** | 1001 – 2000 | **31,106.12** (2x) | **845.27** (NO BONUS) | **676.22** (2x) | **338.12** (2x) |
| **Normal** | 2001+ | 15,553.06 | 845.27 | 338.11 | 169.06 |

**Key Details:**
- **Master Nodes are excluded** from the 2x bonus because they already earned rewards during Blocks 1-1000.
- The extra `16,060.23 OTAI` per block is funded directly by the **Treasury's Genesis Reserve** (2.2B OTAI), ensuring **zero additional inflation** to the total supply.

### 3. The Hardened Compute Score Formula
To prevent hardware spoofing and ghost workers, rewards are calculated using:

`
ComputeUnits = (HardwareScore × UptimeScore) × JobMultiplier × VerifierApproval
`


- **HardwareScore:** Measured via a mandatory **30-second localized benchmark** (TFLOPS/VRAM test). This stops miners from faking high-end GPUs.
- **UptimeScore:** Tracks node reliability. Drops to `0.0` if a node disconnects for more than 10 blocks (5 minutes), preventing ghost workers.
- **JobMultiplier:** `1.0` if idle, `3.5` if actively training an AI model. Rewards real utility.
- **VerifierApproval:** `1.0` if 2/3 verifiers confirm honest work, `0.0` if fraud is detected (slashing applies).

### 4. Client Fee Routing (No Burn)
To keep costs low for AI developers and maximize miner income:

- **75%** of client-paid fees goes directly to the **GPU Worker** that executed the job.
- **25%** goes to **Master Nodes** for routing and validation.
- **0% Burn.** (Deflation is handled separately via the Treasury's quarterly buyback vault).

---

## 🏗️ Node Architecture

| Node Type | Role | Hardware | Reward Source |
| :--- | :--- | :--- | :--- |
| **Master Node** (Validator) | Produces blocks, maintains the full blockchain state, routes P2P traffic, verifies proofs. | High-CPU, 32GB+ RAM, fast SSD. **No GPU required.** | 5% Block Emissions + 25% Client Fees. |
| **GPU Worker** (Miner) | Executes AI training (LoRA/QLoRA) and inference using PyTorch. | High-end GPU (RTX 4090, H100, etc.). | 92% Block Emissions (via Compute Score) + 75% Client Fees. |

**Master Node Staking Requirements:**
- **Minimum Stake:** `10,000 OTAI`.
- **Reward Distribution:** Pro-rata by stake (higher stake = larger share of the 5% pool).
- **Slashing:** Offline or malicious nodes lose up to 20% of their stake (burned).

---

## ⛏️ Halving Schedule & Emission Lifespan

With 30-second block times, ~93.7% of all coins are mined within the first 12 years.

| Era | Timeline | Block Height Range | Base Reward | GPU (92%) | Masters (5%) | Treasury (2%) | Founders (1%) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Era 1** | Years 1–3 | `0` – `3,155,759` | 16,905.50 | 15,553.06 | 845.27 | 338.11 | 169.06 |
| **Era 2** | Years 4–6 | `3,155,760` – `6,311,519` | 8,452.75 | 7,776.53 | 422.63 | 169.05 | 84.53 |
| **Era 3** | Years 7–9 | `6,311,520` – `9,467,279` | 4,226.37 | 3,888.26 | 211.31 | 84.53 | 42.26 |
| **Era 4** | Years 10–12 | `9,467,280` – `12,623,039` | 2,113.18 | 1,944.13 | 105.65 | 42.26 | 21.13 |
| **Era 5** | Years 13–15 | `12,623,040` – `15,778,799` | 1,056.59 | 972.06 | 52.82 | 21.13 | 10.57 |

---

## 🔍 Blockchain Explorer & Tooling

OpenTrainAI is a **standalone Substrate chain**. It does not connect to the Polkadot network, but it uses the **exact same RPC standards** as Polkadot. This means you can use the following tools out-of-the-box:

- **Polkadot-JS Apps:** Point it to your node's WebSocket endpoint (`ws://localhost:9944`) to view blocks, balances, and extrinsics.
- **Statescan (Open-Source):** Deploy your own hosted explorer at `explorer.opentrain.ai` for free.
- **Subscan:** Contact the Subscan team for a dedicated, high-performance explorer (paid integration).
- **Custom Explorers:** Use Substrate's built-in JSON-RPC APIs to build a fully custom frontend.

---

## 🛠️ Tech Stack

- **Layer-1 Node & Consensus:** Rust / Substrate Framework (`libp2p`, RocksDB, JSON-RPC).
- **GPU Worker Client:** Python (`PyTorch`, `huggingface/transformers`, `peft`/LoRA, `vLLM`, `pynvml`).
- **Client & Tooling:** Native CLI Wallet (`opentrain-cli`), REST / WebSocket RPC endpoints.

---

## 🚀 Getting Started (Development)

### Prerequisites
- Rust (latest stable)
- Python 3.10+
- CUDA 12.0+ (for GPU workers)

### Build the L1 Blockchain
```bash
# Clone the repository
git clone https://github.com/opentrainai/opentrain-chain.git
cd opentrain-chain

# Build the Substrate node in release mode
cargo build --release

# Run a local development node
./target/release/opentrain-node --dev
```

---

## Run a GPU Worker

```bash
# Navigate to the worker client
cd opentrain-worker

# Install Python dependencies
pip install -r requirements.txt

# Start the worker (connects to the local node)
python worker.py --node-url http://localhost:9933 --gpu-id 0
```

---

## 📄 License
- This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing
- We welcome contributions! Please read our CONTRIBUTING.md for details on our code of conduct and the process for submitting pull requests.

## ⚠️ Disclaimer
- This software is provided as-is for educational and research purposes. Cryptocurrency investments carry high risk. Please do your own due diligence before participating in the network.

---
