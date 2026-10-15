# Project Plan: Digital Twin Voice Bot with LiveKit & Citations

This plan outlines the design, architecture, and step-by-step implementation for building your Digital Twin Voice Bot. The bot will answer questions about you (using your resume/projects as a source) and provide real-time citations both verbally and visually on the screen.

---

## 1. Project Structure

We will structure the project into three main folders in the workspace:

```
digital-twin-bot/
├── data/                  # Source files for the Digital Twin
│   ├── resume.md          # Markdown version of your resume
│   └── projects.json      # Structured list of your projects and URLs
│
├── backend/               # LiveKit Python Agent
│   ├── agent.py           # Main voice bot logic (LiveKit Agent)
│   ├── rag.py             # Knowledge retrieval and citation parser
│   ├── requirements.txt   # Python dependencies (livekit-agents, openai, etc.)
│   └── .env.example       # Backend environment variables
│
└── frontend/              # Next.js Web Application
    ├── src/
    │   ├── app/           # Next.js Pages & Layout
    │   └── components/    # LiveKit Voice Interface, Waveform, Citation Panel
    ├── package.json       # Frontend dependencies
    └── .env.local.example # Frontend environment variables
```

---

## 2. Technical Stack

*   **Frontend**: Next.js (App Router), Vanilla CSS (or Tailwind if requested), `@livekit/components-react`, `livekit-client`
*   **Backend**: Python 3.10+, `livekit-agents` (Voice Pipeline Agent), `openai` / `langchain` (for RAG & citation parsing), `chromadb` or simple text retrieval (for context search)
*   **APIs Required**:
    *   **LiveKit Cloud**: For WebRTC connection (free tier is perfect)
    *   **OpenAI / Gemini API**: For generating responses
    *   **Deepgram API (Optional)**: High-quality, low-latency STT (default LiveKit providers work too)
    *   **ElevenLabs / Cartesia API (Optional)**: High-quality, expressive TTS (default OpenAI/Google TTS can be used as fallback)

---

## 3. How Citations Will Work

### A. Data Representation
We will store your resume and projects in simple text/Markdown format. For example, `resume.md`:
```markdown
[Section: Education]
Completed Bachelor of Science in Computer Science at University X (2020-2024).

[Section: Work Experience - TechCorp]
Software Engineer Intern at TechCorp (2023). Worked on optimizing database queries.
```

### B. Retrieval & Prompting
1. When the user asks: *"Where did you go to college?"*
2. The RAG system searches `resume.md` and finds the `[Section: Education]` chunk.
3. The LLM receives the prompt:
   ```
   You are the Digital Twin of [Name]. Answer the user's question using the context.
   You must cite your sources by appending [Source Name] to the facts you state.
   Context:
   ---
   [Section: Education] Completed BS in CS at University X.
   ```
4. LLM output: *"I completed my Bachelor of Science in Computer Science at University X [Resume: Education]."*

### C. Live UX Citation Rendering
*   The Python Agent parses the LLM output.
*   It strips out the citation tag `[Resume: Education]` before sending the text to the TTS (so the bot doesn't speak the bracketed text).
*   It sends a JSON payload to the frontend via the LiveKit Data Channel:
    ```json
    {
      "type": "citation",
      "text": "I completed my Bachelor of Science in Computer Science at University X",
      "sources": [
        {
          "name": "Resume: Education",
          "url": "/docs/resume.pdf#page=1"
        }
      ]
    }
    ```
*   The frontend displays a dynamic citation card/pill next to the live transcript.

---

## 4. Step-by-Step Implementation Plan

### Step 1: Initialize Workspace Directories & Data
*   Create `data/` and add a mock profile (or your actual resume/project text if provided).
*   Write scripts to read and search this data.

### Step 2: Build the Backend LiveKit Agent (`backend/`)
*   Set up a standard python virtual environment.
*   Implement `agent.py` using `livekit.agents.pipeline`.
*   Integrate RAG lookup inside the LLM prompt.
*   Add citation parsing and Data Channel signaling.

### Step 3: Build the Frontend (`frontend/`)
*   Initialize a Next.js app in `/frontend`.
*   Build a sleek, premium, responsive UI featuring:
    *   **Interactive Visualizer**: A pulsing Web Audio waveform that moves when you or the bot speaks.
    *   **Live Transcription Panel**: Real-time text display.
    *   **Interactive Citations**: Clickable source links (e.g., viewing the PDF or repo).
    *   **Suggestive Chips**: Clickable buttons with questions like *"What is your stack?"* to help users get started.

### Step 4: Local Testing & Validation
*   Provide a local runner instructions to launch both backend and frontend.
*   Validate WebRTC connections.

---

## 5. Next Actions

Please let me know if you would like me to:
1. Initialize the project directories with a mock profile template.
2. If you want to use your actual profile, please paste your resume or project details in the chat.
