# LiteLLM Gateway Notebook

This repository contains a Jupyter notebook that demonstrates how to use
LiteLLM as a gateway across multiple LLM providers. The notebook walks through
provider setup, direct model calls, fallback routing, token and cost tracking,
local caching, model aliases, and simple load balancing.

## What This Project Covers

- Calling Groq and Gemini models through the same LiteLLM `completion()` API.
- Loading provider credentials from a local `.env` file.
- Comparing responses across providers with shared prompts.
- Using fallback models when a primary model fails.
- Inspecting token usage and estimating request cost.
- Enabling local caching for repeated prompts.
- Creating friendly model aliases with LiteLLM `Router`.
- Distributing requests across multiple deployments with `simple-shuffle`.

## Repository Structure

```text
.
├── gateway_llm.ipynb
└── README.md
```

## Requirements

The notebook uses Python and the following packages:

```bash
pip install litellm langchain langchain-community langchain-openai python-dotenv
```

If you are running inside Jupyter, the first notebook cell includes the same
install command as a commented `%pip` command.

## Environment Variables

Create a `.env` file in the project root and add the provider keys you plan to
use:

```env
GROQ_API_KEY=your_groq_key
GEMINI_API_KEY=your_gemini_key
OPENAI_API_KEY=your_openai_key
```

The notebook checks whether these keys are loaded without printing the secret
values.

## How To Run

1. Open `gateway_llm.ipynb` in Jupyter Notebook, JupyterLab, VS Code, or another
   notebook environment.
2. Install the dependencies if they are not already available.
3. Add the required provider keys to `.env`.
4. Run the notebook cells from top to bottom.

Some sections require specific provider keys. For example, Groq examples require
`GROQ_API_KEY`, Gemini examples require `GEMINI_API_KEY`, and OpenAI router
examples require `OPENAI_API_KEY`.

## Notebook Sections

| Section | Purpose |
| --- | --- |
| Install Required Packages | Documents the dependencies needed for a fresh environment. |
| Import Core Dependencies | Sets up warnings, logging, and LiteLLM imports. |
| Load Provider Credentials | Loads API keys from `.env` and verifies availability. |
| Call Multiple Providers | Sends the same prompt to Groq and Gemini. |
| Compare Providers | Iterates through provider/model pairs with error handling. |
| Configure Fallback Models | Demonstrates retrying on alternate models when a request fails. |
| Track Tokens and Cost | Prints token usage and estimated request cost. |
| Reset State | Clears callbacks and cache before cache testing. |
| Enable Local Caching | Compares first-call provider latency with cached-response latency. |
| Route With Aliases | Maps friendly names to provider-specific model deployments. |
| Load Balance | Distributes requests across a shared model pool. |

## Notes

- Keep `.env` out of version control because it contains credentials.
- Costs shown by LiteLLM are estimates and depend on provider pricing metadata.
- Fallback and router behavior depends on valid model names and available API
  keys.
- The notebook is designed as a learning and prototyping workflow rather than a
  production gateway service.
