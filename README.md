# DeepMeet

DeepMeet is a NiceGUI meeting assistant that uploads meeting audio, transcribes it with Whisper, generates three summary styles, stores results in PostgreSQL, indexes transcript chunks in ChromaDB, and lets users chat with the transcript.

Ollama is the default LLM provider. Cloud providers can be configured from the in-app Settings screen.

## Project Structure

```text
DeepMeet/
  app.py                 # NiceGUI launcher and API registration
  deepmeet/
    api/                 # FastAPI routes mounted into the NiceGUI app
    database/            # PostgreSQL connection, schema, and repository methods
    services/            # STT, LLM, summaries, TTS, vector search, pipeline
    ui/                  # NiceGUI screens
    config.py            # Runtime settings and paths
    models.py            # API payload models
  prompts/               # Executive, short, and detailed summary prompts
  uploads/               # Uploaded audio and generated summary audio
  demo/                  # Left untouched
```

## Features

- NiceGUI workspace with Meetings, Settings, and Postgres views.
- Default local Ollama configuration.
- Settings for provider, model name, API keys, Ollama URL, and voice.
- Audio upload with background processing.
- Executive, short, and detailed summaries.
- Transcript viewer and transcript-aware chat.
- PostgreSQL table browser for meetings, transcripts, summaries, and settings.
- Short-summary text-to-speech audio.

## Setup

```bash
git clone <repository-url>
cd DeepMeet

python -m venv .venv
```

Activate the virtual environment:

**Windows PowerShell**

```powershell
.venv\Scripts\Activate.ps1
```

**macOS/Linux**

```bash
source .venv/bin/activate
```

Install the project dependencies when they are available:

```bash
pip install -r requirements.txt
```

Create a `.env` file with your PostgreSQL connection. API keys are optional when using Ollama.

```env
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=your_password
DB_NAME=deepmeet_db

ACTIVE_LLM_PROVIDER=ollama
LLM_MODEL_NAME=gemma2:2b
OLLAMA_BASE_URL=http://localhost:11434
DEFAULT_TTS_VOICE=en-US-ChristopherNeural
```

Start Ollama and pull the default model if needed:

```bash
ollama pull gemma2:2b
```

Run the app:

```bash
python app.py
```

Open `http://localhost:8080`.

The app also exposes API routes under `/api`, plus legacy-compatible meeting and audio routes at `/meetings`, `/settings`, and `/audio/{filename}`.

## License

See [LICENSE](LICENSE) for license information.
