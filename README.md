# Promptfoo Docker

Self-hosted [Promptfoo](https://www.promptfoo.dev/) web UI and API for running evals and sharing results. Data is stored in `./promptfoo_data` and persists across restarts.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and Docker Compose (or `docker compose` plugin)
- At least one LLM provider API key (e.g. OpenAI, Anthropic, Google) for running evals
- **Option A:** [Git](https://git-scm.com/downloads) (to clone the repo) **or Option B:** a browser (to download the repo as ZIP)

## Quick start

### 1. Get the repo and open the folder

**Option A – With Git (Windows / macOS / Linux):**

```bash
git clone https://github.com/NiftyCall-Tech/promptfoo-docker.git
cd promptfoo-docker
```

**Option B – Without Git (download as ZIP):**

1. Open [https://github.com/NiftyCall-Tech/promptfoo-docker](https://github.com/NiftyCall-Tech/promptfoo-docker) in your browser.
2. Click the green **Code** button → **Download ZIP**.
3. Unzip the file, then open a terminal in the unzipped folder:
   - **Windows:** In File Explorer, go into the `promptfoo-docker` folder, then in the address bar type `cmd` or `powershell` and press Enter. Or right‑click the folder → **Open in Terminal** (if available).
   - **macOS:** Right‑click the `promptfoo-docker` folder → **New Terminal at Folder**, or run `cd ~/Downloads/promptfoo-docker` (adjust path if you saved the ZIP elsewhere).
   - **Linux:** Open a terminal, then run `cd ~/Downloads/promptfoo-docker` (or the path where you extracted the ZIP).

### 2. Create your environment file

**Windows (PowerShell):**

```powershell
Copy-Item .env.example .env
```

**Windows (Command Prompt):**

```cmd
copy .env.example .env
```

**macOS / Linux:**

```bash
cp .env.example .env
```

Edit `.env` and set the API keys you need. Leave others empty. **Do not commit `.env`** - it contains secrets.

### 3. Start the application

**Windows / macOS / Linux:**

```bash
docker compose up -d
```

### 4. Open the UI

Open **http://localhost:3000** in your browser. You can create evals, run them (using the API keys you set in `.env`), and share results.

### 5. Stop the application

```bash
docker compose stop
```

Data in `./promptfoo_data` is kept. To stop and remove the container (data still persists on disk):

```bash
docker compose down
```

## API keys and providers

The most common provider API keys are supported via `.env`. See **`.env.example`** for the full list and [**Promptfoo - LLM Providers**](https://www.promptfoo.dev/docs/providers/) to add any other API keys or providers.

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
  - [Promptfoo Providers](https://www.promptfoo.dev/docs/providers/)
  - [Promptfoo Guides](https://www.promptfoo.dev/docs/category/guides/)
