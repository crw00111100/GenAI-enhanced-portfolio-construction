# Generative AI-enhanced Sector-based Investment Portfolio Construction
## Introduction
This repository contains the updated codes and results for the reseach paper.

The study examines whether Large Language Models (LLMs) could construct financial portfolios that outperform the S&P 500 sector indices. Twelve latest models from leading providers such as OpenAI, Google, Anthropic, DeepSeek and xAI are evaluated for two main tasks:

1. **Stock Selection:** Each model is prompt to select 20 stocks from each of the eleven S&P 500 sector indices.
2. **Weight Assignment:** The selected stocks are then assigned portfolio weights directly by LLMs.

In addition to the weights assigned by LLMs, three optimization techniques (min-variance, max-expected return, max-Sharpe ratio), as well as equal weighted method are applied to the LLM-selected stocks. In total, 660 portolios are constructed and compared with their respective sector indices using multiple performance metrics.

## Install CPLEX solver
For setup instruction, please refer to the [IBM Documentation](https://www.ibm.com/docs/en/icos/22.1.2?topic=cplex-installing)

## Setup API Keys
This project requires API keys from 5 LLM provides, follow the steps below to configure them.

### 1. Obtain API Keys
Create accounts and request API keys from the following providers:
[OpenAI](https://platform.openai.com/account/api-keys)
[Anthropic (Claude)](https://console.anthropic.com/settings/keys)
[Google (Gemini)](https://aistudio.google.com/apikey)
[Deepseek](https://platform.deepseek.com/api_keys)
[xAI (Grok)](https://console.x.ai/team/256ef55d-0d0c-43bd-bff2-955a28debfbd/api-keys)

### 2. Store the Keys
1. Inside the root dictionary of the project, create a folder called ``api_key``.
2. For each provider, create a text file inside the ``api_key`` folder with the filenames below:
    api_key
    ├── anthropic_api_key.txt
    ├── deepseek_api_key.txt
    ├── gemini_api_key.txt
    ├── grok_api_key.txt
    └── openai_api_key.txt
3. Copy your API key to its corresponding file

## Overall Workflow
As the final experiment is based on a portfolio size of 20 stocks, modules with names containing ``15stocks`` are deprecated and should not be run.

Moreover, time splits in October 2024 and an out-of-sample period of 6 months for the January 2025 split were tested during the experiments but were not included in the paper. Therefore, modules with names containing ``Oct split`` or ``Jan split_6months`` are not necessary to run.

1. [portfolio_construction_20stocks.ipynb](portfolio_construction_20stocks.ipynb): construct the portfolio with different LLMs.
2. [portfolio_analysis_20stocks_Jan split.ipynb](<portfolio_analysis_20stocks_Jan split.ipynb>): apply optimization techniques and analysis the portfolio constructed by LLMs with the in/out of-sample split time at January 2025.
3. [portfolio_analysis_20stocks_Apr split.ipynb](<portfolio_analysis_20stocks_Apr split.ipynb>): apply optimization techniques and analysis the portfolio constructed by LLMs with the in/out of-sample split time at April 2025.
4. [summary_metrics.ipynb](summary_metrics.ipynb): notebook to plot the summary metrics comparing the performance of portfolios with corresponding benchmarks.
5. [metrics_analysis.ipynb](metrics_analysis.ipynb): Analyzing portfolio's performance using various evaluation metrics.

In module [portfolio_construction_20stocks.ipynb](portfolio_construction_20stocks.ipynb), under the sections LLM API and Weighted Portfolio, you will find several sub-sections corresponding to different LLM models. Please execute only the code blocks under the sub-section of the specific model you intend to use.

## Files and Folders
[4_returns_insample/](4_returns_insample): In-sample (5 years prior to the split time) stock returns from S&P 500 sector indices.
[4_returns_outsample/](4_returns_outsample): Out-of-sample stock returns, beginning in January 2025 or April 2025, each with a 3-month testing window.
[cached/](cached): Cached LLM responses for portfolio construction and optimization.
[difference/](difference): data of the difference between benchmark (index) and portfolio for summary metrics plotting.
[metrics/](metrics): related csv outputs for computed performance metrics.
[SP500.csv](SP500.csv): List of companies in S&P 500 index.