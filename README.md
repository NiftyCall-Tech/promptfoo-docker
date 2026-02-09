# Promptfoo Docker

Self-hosted [Promptfoo](https://www.promptfoo.dev/) web UI and API for running evals and sharing results. Data is stored in `./promptfoo_data` and persists across restarts.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and Docker Compose (or `docker compose` plugin)
- At least one LLM provider API key (e.g. OpenAI, Anthropic, Google) for running evals

## Quick start

### 1. Create your environment file

```bash
cp .env.example .env
```

Edit `.env` and set the API keys you need. Leave others empty. **Do not commit `.env`** — it contains secrets.

### 2. Start the application

```bash
docker compose up -d
```

### 3. Open the UI

Open **http://localhost:3000** in your browser. You can create evals, run them (using the API keys you set in `.env`), and share results.

### 4. Stop the application

```bash
docker compose stop
```

Data in `./promptfoo_data` is kept. To stop and remove the container (data still persists on disk):

```bash
docker compose down
```

## API keys and providers

The most common provider API keys are supported via `.env`. See **`.env.example`** for the full list and [**Promptfoo – LLM Providers**](https://www.promptfoo.dev/docs/providers/) to add any other API keys or providers.

Examples of variables you can set in `.env`:

| Provider   | Environment variable     |
|-----------|---------------------------|
| OpenAI    | `OPENAI_API_KEY`          |
| Anthropic | `ANTHROPIC_API_KEY`       |
| Google    | `GOOGLE_API_KEY`          |
| OpenRouter| `OPENROUTER_API_KEY`      |
| DeepSeek  | `DEEPSEEK_API_KEY`        |
| Mistral   | `MISTRAL_API_KEY`         |
| Groq      | `GROQ_API_KEY`            |
| Others    | See [docs](https://www.promptfoo.dev/docs/providers/) |

## Data and volumes

- **Host path:** `./promptfoo_data` is mounted into the container. Create it manually if you like; Docker Compose will create it when the container starts if needed.
- **Named volume:** You can switch to a Docker-managed volume by following the commented instructions in `docker-compose.yml`.

## Troubleshooting

- **Docker not found / “cannot find the file specified”**  
  Start Docker Desktop (or your Docker daemon) and wait until it is fully running, then run `docker compose up -d` again.

- **Evals or UI not loading**  
  Ensure at least one provider API key is set in `.env` if you want to run evals from the UI.

- **More help**  
  [Promptfoo – Providers](https://www.promptfoo.dev/docs/providers/)
