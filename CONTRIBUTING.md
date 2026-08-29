# Contributing to OpenTrainAI ($OTAI)

First off, thank you for considering contributing to OpenTrainAI! 🚀 

We are building the first decentralized Proof-of-Useful-Work (PoUW) Layer-1 for AI compute, and every contribution—whether it's a bug fix, a new feature, or improving our documentation—helps push decentralized AI forward.

Please take a moment to review this document to make the contribution process easy and effective for everyone involved.

---

## 📜 Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](./CODE_OF_CONDUCT.md). We are committed to providing a friendly, safe, and welcoming environment for all contributors.

---

## 🛠️ Prerequisites

Before you start contributing, ensure you have the following installed:

| Requirement | Version | Purpose |
| :--- | :--- | :--- |
| **Rust** | Latest Stable | Core L1 Blockchain (Substrate) |
| **Cargo** | Latest Stable | Rust Package Manager |
| **Python** | 3.10+ | GPU Worker Client & Scripts |
| **Pip / Poetry** | Latest | Python Dependency Management |
| **Docker** | 20.10+ | Containerized Testing & Localnet |
| **Git** | 2.30+ | Version Control |
| **CUDA** | 12.0+ | (Optional) For GPU Worker development |

---

## 🧬 Project Structure

Understanding the repository structure will help you find your way around:

```
opentrain-chain/
├── pallets/                     # Custom Substrate Pallets (PoUW logic, Staking, Rewards)
│   ├── powu/                    # Core Proof-of-Useful-Work logic
│   ├── master-node/             # Master Node staking & slashing
│   └── treasury/                # Treasury & Buyback Vault
├── runtime/                     # OpenTrainAI Runtime (WASM)
│   └── src/
│       └── lib.rs               # Runtime composition
├── node/                        # Substrate Node (CLI, RPC, Service)
│   └── src/
│       └── service.rs           # Node service & chain specification
├── opentrain-worker/            # Python GPU Worker Client
│   ├── worker.py                # Main entry point
│   ├── trainer/                 # LoRA/QLoRA training logic
│   ├── verifier/                # Proof verification logic
│   └── requirements.txt
├── scripts/                     # Development & testing utilities
├── docs/                        # Technical documentation
└── Cargo.toml                   # Workspace configuration
```

---

## 🚀 How to Contribute

### 1. Reporting Bugs (Issues)

If you find a bug, please open a [GitHub Issue](https://github.com/opentrainai/opentrain-chain/issues) and include:

- **A clear title** and a detailed description.
- **Steps to reproduce** the bug.
- **Expected behavior** vs. **Actual behavior**.
- **Screenshots or logs** if applicable (use `RUST_LOG=debug` or Python stack traces).
- **Environment details:** OS, Rust version, CUDA version.

### 2. Suggesting Enhancements

We welcome feature requests and improvements! When suggesting a new feature:

- **Explain the problem** this feature will solve.
- **Describe the solution** you'd like to see.
- **Explain why** this is valuable for the OpenTrainAI network (e.g., improves security, miner earnings, or developer experience).

### 3. Submitting Code (Pull Requests)

We use a **GitHub Flow** workflow:

1. **Fork the repository** and create your branch from `main`.
2. **Name your branch** descriptively, e.g.,:
   - `feat/add-gpu-benchmark`
   - `fix/master-node-slashing`
   - `docs/update-readme`
3. **Write code that is tested** (see [Testing](#-testing) below).
4. **Format your code** (see [Coding Standards](#-coding-standards) below).
5. **Commit your changes** with a clear commit message.
6. **Push to your fork** and open a Pull Request (PR) against the `main` branch of the main repository.
7. **Fill out the PR template** completely, linking any relevant issues.

---

## 📝 Coding Standards

### Rust (L1 Node & Pallets)

- **Formatting:** Always run `cargo fmt` before committing.
- **Linting:** Run `cargo clippy --all-targets -- -D warnings` to catch common mistakes.
- **Documentation:** Add `#[doc]` comments for all public functions, structs, and pallet extrinsics.
- **Error Handling:** Use `sp_runtime::DispatchError` for pallet errors; use `anyhow` or `thiserror` for off-chain utilities.
- **Naming:**
  - Structs/Enums: `PascalCase`
  - Functions/Variables: `snake_case`
  - Constants: `SCREAMING_SNAKE_CASE`

**Example:**
```rust
/// This function calculates the hardened Compute Score for a worker.
pub fn calculate_compute_score(
    hardware_score: f32,
    uptime_score: f32,
    job_multiplier: f32,
) -> f32 {
    hardware_score * uptime_score * job_multiplier
}
```

### Python (GPU Worker Client)

- **Formatting:** Use `black` and `isort` to automatically format code.
- **Linting:** Use `pylint` or `ruff` to catch style and logic issues.
- **Type Hints:** Always use type hints for function arguments and return values.
- **Docstrings:** Use Google-style docstrings for all public classes and methods.

**Example:**
```python
def run_lora_training(
    model_name: str,
    dataset_path: str,
    learning_rate: float = 2e-4,
) -> LoRAResult:
    """
    Runs a LoRA fine-tuning job on the specified model.

    Args:
        model_name: Hugging Face model identifier (e.g., 'meta-llama/Llama-3.2-3B').
        dataset_path: Local path to the training dataset (JSONL format).
        learning_rate: Learning rate for the optimizer.

    Returns:
        LoRAResult: The trained adapter weights and training metrics.
    """
    # Implementation here
```

---

## 🧪 Testing

### Rust Unit & Integration Tests

- Run all Rust tests:
  ```bash
  cargo test --all
  ```
- Run a specific pallet test:
  ```bash
  cargo test -p pallet-pouw
  ```
- Ensure your code **compiles to WASM** without errors:
  ```bash
  cargo build --release --target wasm32-unknown-unknown
  ```

### Python Tests (Worker Client)

- We use `pytest` for the worker client.
- Run all Python tests:
  ```bash
  cd opentrain-worker
  pytest tests/
  ```
- Ensure all tests pass **without GPU** (use CPU fallback for CI) and **with GPU** (for local development).

---

## 📧 Commit Message Guidelines

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

- **Format:** `<type>(<scope>): <subject>`
- **Types:**
  - `feat`: New feature
  - `fix`: Bug fix
  - `docs`: Documentation updates
  - `style`: Code style/formatting (no functional change)
  - `refactor`: Code refactoring
  - `perf`: Performance improvements
  - `test`: Adding/updating tests
  - `chore`: Build process, CI/CD, tooling

**Examples:**
- `feat(pouw): add 30-second mandatory hardware benchmark`
- `fix(master-node): correct slashing calculation for offline nodes`
- `docs(readme): update tokenomics with final 92/5/2/1 split`

---

## 📜 Developer Certificate of Origin (DCO)

We require all contributors to sign off on their commits to certify that they have the right to submit the code under the MIT License.

To sign off, add `Signed-off-by: Your Name <your.email@example.com>` to your commit message. You can do this automatically using the `-s` flag:

```bash
git commit -s -m "feat(pouw): add benchmark verification logic"
```

This certifies that you wrote the code or have the right to contribute it, and you agree to the [DCO](https://developercertificate.org/).

---

## 🔄 Pull Request Review Process

1. **At least one maintainer** must review and approve your PR.
2. **All CI checks** must pass (Rust fmt, Clippy, Python linting, unit tests, and WASM compilation).
3. **Changes may be requested**—please address them promptly.
4. Once approved, a maintainer will merge your PR into `main`.

---

## 🌟 Recognition

We appreciate every contribution! Contributors who make significant improvements will be added to our [CONTRIBUTORS.md](./CONTRIBUTORS.md) file and featured in our ecosystem updates.

---

## ❓ Need Help?

- **GitHub Issues:** Use the issue tracker for bugs or feature requests.
- **Discord / Telegram:** (Link to your community server).
- **Documentation:** Check the `docs/` folder for detailed architectural guides.

Thank you for helping us build the future of decentralized AI compute! 🧠⚡
