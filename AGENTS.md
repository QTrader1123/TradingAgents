## Cursor Cloud specific instructions

TradingAgents is a single Python CLI and library. There is no web server or database to start. Standard lint, test, and run commands are in the README and `.github/workflows/ci.yml` (`ruff check .`, `pytest -q`, `tradingagents`).

- The cloud dev environment uses a gitignored virtualenv at `.venv` (Python 3.12). Activate it with `source .venv/bin/activate` before `ruff`, `pytest`, or `tradingagents`. Creating that venv needs the `python3.12-venv` apt package.
- `pytest` refuses outbound network unless a test is marked `integration` (`tests/conftest.py`). The suite does not need an LLM key. One DeepSeek test skips without `DEEPSEEK_API_KEY`, and the Bedrock test skips unless `pip install ".[bedrock]"` has been run.
- `tradingagents` (and `python -m cli.main`) is interactive and needs a real TTY. `tradingagents --help` and `tradingagents backtest` do not. A live analysis needs one LLM provider key (default `OPENAI_API_KEY` in `.env`). Yahoo Finance market data needs outbound HTTPS and no key.
