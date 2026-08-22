# OpenTrainAI ($OTAI)

OpenTrainAI is a decentralized Proof-of-Useful-Work (PoUW) compute network designed to make consumer-grade GPUs profitable by crowdsourcing AI training, fine-tuning, and inference workloads.

Unlike traditional proof-of-work networks that waste electricity on arbitrary hashing algorithms, OpenTrainAI rewards node operators for completing real-world AI tasks based on total execution time, compute complexity, and node reliability.

---

## Core Features

* **Proof-of-Useful-Work (PoUW) Mining:** GPU operators earn `$OTAI` by serving micro-inference API calls, executing parameter-efficient fine-tuning (LoRA/QLoRA) steps, and running data embeddings.
* **Execution & Time-Based Rewards:** Node rewards are calculated based on job execution time, compute difficulty rating, and uptime verification.
* **Protocol Halving Schedule:** Programmatically halves token emissions at fixed intervals to enforce long-term scarcity and control supply inflation.
* **Automated Fee Splits:** Built-in protocol-level revenue routing directs fees from task payouts to support development and long-term ecosystem growth.

---

## Tokenomics ($OTAI)

* **Token Ticker:** `$OTAI`
* **Total Max Supply:** `110,000,000,000` (110 Billion)
* **Token Type:** ERC-20 / SPL Standard (Fully Tradeable on Decentralized & Centralized Exchanges)

### Supply Allocation

| Pool | Percentage | Token Allocation | Purpose |
| --- | --- | --- | --- |
| **Mining & Compute Rewards** | 97.0% | 106,700,000,000 $OTAI | Distributed to active GPU workers via task execution and uptime |
| **Development Treasury** | 2.0% | 2,200,000,000 $OTAI | Infrastructure, node verification servers, and development grants |
| **Founders Reserve** | 1.0% | 1,100,000,000 $OTAI | Core protocol founders allocation |

### Emission & Fee Mechanics

For every task completion payout or network block emission, payouts are auto-routed at the smart contract level:

* **97%** goes directly to the GPU Worker Node.
* **2%** goes directly to the Development Treasury Wallet.
* **1%** goes directly to the Founders Fee Wallet.

---

## How Mining Works

1. **Job Submission:** Developers post AI micro-tasks (inference, fine-tuning, embedding) using `$OTAI` tokens.
2. **Task Assignment:** The network orchestrator assigns jobs to GPU nodes matched to their available VRAM (supporting RTX 3060/4060/4070+ consumer cards up to enterprise GPUs).
3. **Execution & Proof Submission:** The worker node executes the workload, logging execution duration and generating output proofs.
4. **Reward Distribution:** Once verified, the contract calculates the reward based on execution time and compute difficulty, issuing the payout according to the 97/2/1 allocation split.

---

## Halving Mechanics

To protect token value over time, task reward rates undergo halving at predetermined milestones (e.g., every fixed block interval or task completion threshold). This reduces supply expansion as network demand increases, encouraging early hardware adoption.

---

## Market & Trading Support

`$OTAI` is designed around standard ERC-20 / SPL token interfaces:

* Fully compatible with decentralized exchange liquidity pools (e.g., Uniswap, PancakeSwap, Raydium).
* Users can buy, sell, or trade `$OTAI` seamlessly using standard Web3 wallets like MetaMask or Phantom.

---

## Tech Stack

* **Worker Node Engine:** Python (PyTorch, Hugging Face `transformers`, `peft`, vLLM)
* **Orchestration & Network Layer:** Rust / Go / C (`libp2p`, gRPC)
* **Smart Contracts & Tokenomics:** Solidity / Rust (OpenZeppelin standards, automated fee-splitting)

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.
