# LLM Analysis Quiz Solver

An autonomous agent built with LangGraph and LangChain to solve multi-step data quizzes using web scraping, data processing, analysis, and visualization. Uses Google Gemini 2.5 Flash model to orchestrate tasks.

---

## Features

- Autonomous multi-step quiz solving
- Scrapes JavaScript-heavy pages using Playwright
- Executes Python code for data tasks
- Downloads and processes files (PDFs, CSVs, images)
- Dynamic dependency installation
- Docker-ready deployment

---

## Project Structure

```
final-tds-project-2/
├── main.py
├── agent.py
├── pyproject.toml
├── Dockerfile
├── .env
├── tools/
│   ├── __init__.py
│   ├── web_scraper.py
│   ├── code_generate_and_run.py
│   ├── download_file.py
│   ├── send_request.py
│   └── add_dependencies.py
└── README.md
```

---

## Installation

### Step 1: Clone

```bash
git clone https://github.com/23f3001596-star/final-tds-project-2.git
cd final-tds-project-2
```

### Step 2: Install Dependencies

#### Option A: Using `uv`

```bash
pip install uv
uv sync
uv run playwright install chromium
uv run main.py
```

#### Option B: Using `pip`

```bash
python -m venv venv
.\venv\Scripts\activate  # Windows
# source venv/bin/activate  # macOS/Linux
pip install -e .
playwright install chromium
python main.py
```

---

## Configuration

Create a `.env` file:

```env
EMAIL=your.email@example.com
SECRET=your_secret_string
GOOGLE_API_KEY=your_gemini_api_key
```

### Getting a Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Create a new API key
3. Copy it into your `.env` file

---

## Usage

### Local Development

Start the FastAPI server:

```bash
# If using uv
uv run main.py

# If using standard Python
python main.py
```

Server runs at: `http://0.0.0.0:7860`

### Testing the Endpoint

Send a POST request:

```bash
curl -X POST http://localhost:7860/solve \
  -H "Content-Type: application/json" \
  -d '{
    "email": "your.email@example.com",
    "secret": "your_secret_string",
    "url": "https://tds-llm-analysis.s-anand.net/demo"
  }'
```

Expected response:

```json
{
  "status": "ok"
}
```

---

## API Endpoints

### POST `/solve`

Request Body:

```json
{
  "email": "your.email@example.com",
  "secret": "your_secret_string",
  "url": "https://example.com/quiz-123"
}
```

**Responses:**

| Status Code | Description                    |
| ----------- | ------------------------------ |
| 200         | Secret verified, agent started |
| 400         | Invalid JSON payload           |
| 403         | Invalid secret                 |

### GET `/healthz`

Health check endpoint:

```json
{
  "status": "ok",
  "uptime_seconds": 3600
}
```

---

## Docker Deployment

### Build the Image

```bash
docker build -t llm-analysis-agent .
```

### Run the Container

```bash
docker run -p 7860:7860 \
  -e EMAIL="your.email@example.com" \
  -e SECRET="your_secret_string" \
  -e GOOGLE_API_KEY="your_api_key" \
  llm-analysis-agent
```

### Deploy to HuggingFace Spaces

1. Create a new Space with Docker SDK
2. Push this repository to your Space
3. Add secrets in Space settings:
   - `EMAIL`
   - `SECRET`
   - `GOOGLE_API_KEY`
4. The Space will automatically build and deploy

---

## 📝 License

This project is licensed under the MIT License.

---

**Author**: Nikhita Kunisetti\
**Course**: Tools in Data Science (TDS), IIT Madras

GitHub: [final-tds-project-2](https://github.com/23f3001596-star/final-tds-project-2)



