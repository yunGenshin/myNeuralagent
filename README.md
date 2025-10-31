### 我希望通过修改neuralagent自定义一些我想要的功能，这个工作还没开始，下面是neuralagent的介绍：
![NeuralAgent](docs/images/neuralagent_logo.png)

**NeuralAgent** is your AI personal assistant that actually *gets things done*. It lives on your desktop, types, clicks, navigates the browser, fills out forms, sends emails, and performs tasks automatically using modern large language models — all powered by a fast, extensible, and open architecture.

> Real productivity. Not just conversation.

---

![Demo](docs/images/demo.gif)

---

## 🌐 Website & Community

- 🌍 **Website**: [https://www.getneuralagent.com](https://www.getneuralagent.com)
- 💬 **Discord**: [Join NeuralAgent Discord](https://discord.gg/eGyW3kPcUs)

---

## 🚀 Features

- ✅ Desktop automation with `pyautogui`
- ✅ Background automation (Windows Only For Now) via WSL (browser-only).
- ✅ Supports Claude, GPT-4, Azure OpenAI, and Bedrock
- ✅ Modular agents: Planner, Classifier, Suggestor, Title, and more
- ✅ Multimodal (text + vision)
- ✅ FastAPI backend + Electron + React frontend

---

## 🖥️ Project Structure

```
neuralagent/
├── backend/              # FastAPI + Postgres backend
├── desktop/              # ElectronJS desktop app
│   └── neuralagent-app/  # React frontend inside Electron
│   └── aiagent/          # Python code (pyautogui)
└── README.md
```

---

## ⚙️ Setup Instructions

> 🧪 Open **two terminal windows** – one for `backend` and one for `desktop`.

---

### 🐍 Backend Setup

1. **Create and activate a virtual environment (optional but recommended):**

```bash
cd backend
python -m venv venv
# Activate:
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate     # Windows
```

2. **Install requirements:**

```bash
pip install -r requirements.txt
```

3. **Create a local Postgres database.**

4. **Copy `.env.example` to `.env` and fill in:**

```env
DB_HOST=
DB_PORT=
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=
DB_CONNECTION_STRING=

JWT_ISS=NeuralAgentBackend
JWT_SECRET=

REDIS_CONNECTION=

# Optional: For Bedrock
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
BEDROCK_REGION=us-west-2

# Optional: For Azure OpenAI
AZURE_OPENAI_ENDPOINT=
AZURE_OPENAI_API_KEY=
OPENAI_API_VERSION=2024-12-01-preview

# Optional: OpenAI/Anthropic
OPENAI_API_KEY=
ANTHROPIC_API_KEY=

# Model config per agent
CLASSIFIER_AGENT_MODEL_TYPE=openai|azure_openai|anthropic|bedrock
CLASSIFIER_AGENT_MODEL_ID=gpt-4.1

TITLE_AGENT_MODEL_TYPE=openai|azure_openai|anthropic|bedrock
TITLE_AGENT_MODEL_ID=gpt-4.1-nano

SUGGESTOR_AGENT_MODEL_TYPE=openai|azure_openai|anthropic|bedrock
SUGGESTOR_AGENT_MODEL_ID=gpt-4.1-mini

PLANNER_AGENT_MODEL_TYPE=openai|azure_openai|anthropic|bedrock
PLANNER_AGENT_MODEL_ID=gpt-4.1

COMPUTER_USE_AGENT_MODEL_TYPE=openai|azure_openai|anthropic|bedrock
COMPUTER_USE_AGENT_MODEL_ID=us.anthropic.claude-sonnet-4-20250514-v1:0

LANGCHAIN_TRACING_V2=false
LANGCHAIN_ENDPOINT=
LANGCHAIN_API_KEY=
LANGCHAIN_PROJECT=

# Google Login
GOOGLE_LOGIN_CLIENT_ID=
GOOGLE_LOGIN_CLIENT_SECRET=
GOOGLE_LOGIN_DESKTOP_REDIRECT_URI=http://127.0.0.1:36478
```

5. **Run database migrations:**

```bash
alembic upgrade head
```

6. **Start the backend server:**

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

---

### 🖥️ Frontend (Desktop + Electron) Setup

1. **Install dependencies in the Electron root:**

```bash
cd desktop
npm install
```

2. **Navigate to the React app:**

```bash
cd neuralagent-app
```

3. **Copy `.env.example` to `.env` and fill in:**

```env
REACT_APP_PROTOCOL=http
REACT_APP_WEBSOCKET_PROTOCOL=ws
REACT_APP_DNS=127.0.0.1:8000
REACT_APP_API_KEY=
```

4. **Go back to the desktop root:**

```bash
cd ..
```

5. **Set up the local AI agent daemon (Python service):**
```bash
cd aiagent
python -m venv venv
source venv/bin/activate  # Or use `venv\Scripts\activate` on Windows
pip install -r requirements.txt
deactivate
```

6. **Start the Electron desktop app:**

```bash
cd ..
npm start
```

---

## 🤖 Agents & Model Providers

You can configure different model providers (`OpenAI`, `Azure OpenAI`, `Anthropic`, `Bedrock`) per agent in `.env`.  
Agent types include:

- `PLANNER_AGENT`
- `CLASSIFIER_AGENT`
- `TITLE_AGENT`
- `SUGGESTOR_AGENT`
- `COMPUTER_USE_AGENT`

---

## 📣 Contributing

We welcome pull requests and community contributions!

---

## 🛡️ License

MIT License.  
Use at your own risk. This tool moves your mouse and types on your behalf — test responsibly!

---

## 💬 Questions?

Feel free to open an issue or start a discussion.
