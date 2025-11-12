<!-- PROJECT SHIELDS -->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git">
    <img src="docs/images/cli.png" alt="Logo" width="466" height="262">
  </a>

<h3 align="center">Polymarket Agents</h3>

  <p align="center">
    Trade autonomously on Polymarket using AI Agents
    <br />
    <a href="https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git">View Demo</a>
    ·
    <a href="https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    ·
    <a href="https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>


<!-- CONTENT -->
# Polymarket Agents

Polymarket Agents is a developer framework and set of utilities for building AI agents for Polymarket.

This code is free and publicly available under MIT License open source license ([terms of service](#terms-of-service))!

## Features

- **AI-Powered Trading**: Autonomous trading agents using state-of-the-art LLMs
- **Polymarket Integration**: Full API integration for markets, events, and trading
- **RAG Support**: Local and remote RAG (Retrieval-Augmented Generation) for market analysis
- **Data Sources**: Integration with news providers, web search, and betting services
- **Superforecasting**: Advanced prediction capabilities using superforecaster methodologies
- **Modern Stack**: Built with Python 3.12+, LangChain, FastAPI, and modern tooling
- **Docker Ready**: Containerized deployment for easy setup

# Getting started

This project requires **Python 3.12+**.

## Prerequisites

- Python 3.12 or higher
- pip (Python package manager)
- (Optional) Docker for containerized deployment

## Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/BlackSky-Jose/PolyMarket-AI-agent-trading.git
   cd poly-ai-trading-agent
   ```

2. **Create a virtual environment**

   Using `venv` (recommended):
   
   ```bash
   python -m venv .venv
   ```

   Or using `uv` (faster):
   
   ```bash
   uv venv
   ```

3. **Activate the virtual environment**

   - On Windows (PowerShell):
   
   ```powershell
   .venv\Scripts\Activate.ps1
   ```
   
   - On Windows (CMD):
   
   ```cmd
   .venv\Scripts\activate.bat
   ```

   - On macOS and Linux:
   
   ```bash
   source .venv/bin/activate
   ```

4. **Install the project**

   Using pip:
   
   ```bash
   pip install -e .
   ```
   
   Or with development dependencies:
   
   ```bash
   pip install -e ".[dev]"
   ```

   Using uv (faster):
   
   ```bash
   uv pip install -e ".[dev]"
   ```

5. **Set up environment variables**

   Create a `.env` file in the project root:
   
   ```bash
   # Copy example if available, or create new
   touch .env
   ```
   
   Add the following environment variables:
   
   ```env
   POLYGON_WALLET_PRIVATE_KEY="your_private_key_here"
   OPENAI_API_KEY="your_openai_api_key_here"
   NEWSAPI_API_KEY="your_newsapi_key_here"  # Optional
   TAVILY_API_KEY="your_tavily_key_here"     # Optional
   ```

6. **Load your wallet with USDC** (if trading)

## Usage

### Command Line Interface

The CLI provides various commands for interacting with Polymarket:

```bash
# List available commands
python -m scripts.python.cli --help

# Get all markets
python -m scripts.python.cli get-all-markets --limit 10 --sort-by spread

# Get all events
python -m scripts.python.cli get-all-events --limit 5

# Query LLM
python -m scripts.python.cli ask-llm "What are the best markets to trade?"

# Run autonomous trader (⚠️ Review TOS first)
python -m scripts.python.cli run-autonomous-trader
```

### Direct Script Execution

You can also run the trading script directly:

```bash
python -m agents.application.trade
```

### Docker Deployment

Build and run with Docker:

```bash
# Build the image
docker build -t poly-ai-trading-agent .

# Run the container
docker run --env-file .env poly-ai-trading-agent
```

Or use the provided scripts:

```bash
./scripts/bash/build-docker.sh
./scripts/bash/run-docker-dev.sh
```

## Development

### Code Quality

This project uses modern Python tooling:

- **Ruff** - Fast Python linter and formatter
- **mypy** - Static type checking
- **pre-commit** - Git hooks for code quality

Set up pre-commit hooks:

```bash
pre-commit install
```

Run linting and type checking:

```bash
ruff check .
ruff format .
mypy .
```

### Testing

Run tests:

```bash
pytest
```

## Architecture

The Polymarket Agents architecture features modular components that can be maintained and extended by individual community members.

### APIs

Polymarket Agents connectors standardize data sources and order types.

- `Chroma.py`: chroma DB for vectorizing news sources and other API data. Developers are able to add their own vector database implementations.

- `Gamma.py`: defines `GammaMarketClient` class, which interfaces with the Polymarket Gamma API to fetch and parse market and event metadata. Methods to retrieve current and tradable markets, as well as defined information on specific markets and events.

- `Polymarket.py`: defines a Polymarket class that interacts with the Polymarket API to retrieve and manage market and event data, and to execute orders on the Polymarket DEX. It includes methods for API key initialization, market and event data retrieval, and trade execution. The file also provides utility functions for building and signing orders, as well as examples for testing API interactions.

- `Objects.py`: data models using Pydantic; representations for trades, markets, events, and related entities.

### Scripts

Files for managing your local environment, server set-up to run the application remotely, and cli for end-user commands.

`cli.py` is the primary user interface for the repo. Users can run various commands to interact with the Polymarket API, retrieve relevant news articles, query local data, send data/prompts to LLMs, and execute trades in Polymarkets.

Commands should follow this format:

`python scripts/python/cli.py command_name [attribute value] [attribute value]`

Example:

`get-all-markets`
Retrieve and display a list of markets from Polymarket, sorted by volume.

   ```
   python scripts/python/cli.py get-all-markets --limit <LIMIT> --sort-by <SORT_BY>
   ```

- limit: The number of markets to retrieve (default: 5).
- sort_by: The sorting criterion, either volume (default) or another valid attribute.

# Contributing

If you would like to contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

### Code Quality

Before making contributions, please:

1. Install development dependencies: `pip install -e ".[dev]"`
2. Set up pre-commit hooks: `pre-commit install`
3. Run linting: `ruff check . && ruff format .`
4. Run type checking: `mypy .`


# Prediction markets reading

- Prediction Markets: Bottlenecks and the Next Major Unlocks, Mikey 0x: https://mirror.xyz/1kx.eth/jnQhA56Kx9p3RODKiGzqzHGGEODpbskivUUNdd7hwh0
- The promise and challenges of crypto + AI applications, Vitalik Buterin: https://vitalik.eth.limo/general/2024/01/30/cryptoai.html
- Superforecasting: How to Upgrade Your Company's Judgement, Schoemaker and Tetlock: https://hbr.org/2016/05/superforecasting-how-to-upgrade-your-companys-judgment

# Contact

For any questions or inquiries, please contact liam@polymarket.com or reach out at www.greenestreet.xyz

Enjoy using the CLI application! If you encounter any issues, feel free to open an issue on the repository.

# Terms of Service

[Terms of Service](https://polymarket.com/tos) prohibit US persons and persons from certain other jurisdictions from trading on Polymarket (via UI & API and including agents developed by persons in restricted jurisdictions), although data and information is viewable globally.



