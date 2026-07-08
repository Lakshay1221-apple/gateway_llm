# LiteLLM Gateway Notebook

This repository contains a Jupyter notebook that demonstrates how to use
LiteLLM as a gateway across multiple LLM providers. The notebook walks through
provider setup, direct model calls, fallback routing, token and cost tracking,
local caching, model aliases, load balancing, observability callbacks,
LangChain integration, task-aware routing, and input guardrails.

## What This Project Covers

- Calling Groq and Gemini models through the same LiteLLM `completion()` API.
- Loading provider credentials from a local `.env` file.
- Comparing responses across providers with shared prompts.
- Using fallback models when a primary model fails.
- Inspecting token usage and estimating request cost.
- Enabling local caching for repeated prompts.
- Creating friendly model aliases with LiteLLM `Router`.
- Distributing requests across multiple deployments with `simple-shuffle`.
- Comparing least-busy, latency-aware, and cost-aware routing patterns.
- Capturing request metadata with LiteLLM callbacks.
- Calling LiteLLM models from LangChain using `ChatLiteLLM`.
- Applying simple guardrails for PII redaction, prompt injection, and blocked
  topics.

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

The LangChain integration examples also require:

```bash
pip install langchain-litellm
```

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
| Least-Busy Routing | Routes requests toward deployments with lower current load. |
| Latency-Based Routing | Prefers deployments with lower observed response times. |
| Cost-Aware Routing | Compares models with different expected price profiles. |
| LiteLLM Callbacks | Records prompt, token, latency, cost, and user metadata. |
| LangChain Adapter | Uses `ChatLiteLLM` inside a standard LangChain chain. |
| LangChain Fallbacks | Adds model fallbacks with LangChain's `with_fallbacks()`. |
| Smart Router | Classifies tasks and chooses model chains for each task type. |
| PII Guardrail | Redacts sensitive data before sending prompts to a model. |
| Prompt Injection Guardrail | Blocks common prompt-injection and jailbreak attempts. |
| Topic Guardrail | Refuses requests that match restricted keyword categories. |

## Notes

- Keep `.env` out of version control because it contains credentials.
- Costs shown by LiteLLM are estimates and depend on provider pricing metadata.
- Fallback and router behavior depends on valid model names and available API
  keys.
- Guardrail examples are intentionally simple and should be expanded before
  production use.
- The notebook is designed as a learning and prototyping workflow rather than a
  production gateway service.
