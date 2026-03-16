

**Google Technologies:**
- **Gemini Live API** — the core of the Live Cue Card system. Bidirectional audio streaming, real-time transcription, and behavioral analysis at sub-200ms latency
- **Agent Development Kit (ADK)** — orchestrates two specialized agents: the Live Session Agent (Cue Cards) and the Career Intelligence Agent (Scorecards + Deal Board health analysis)
- **Vertex AI** — hosts the behavioral benchmark models used to score sessions against career-stage-specific playbook standards
- **Cloud Firestore** — stores session transcripts, behavioral analysis results, personal coaching history, and the data that trains the personal playbook over time
- **Cloud Storage** — archives session audio for Highlight Reel and Danger Moment playback in scorecards
- **Cloud Run** — containerized deployment of the PHP backend and WebSocket server with auto-scaling
- **Google Meet MCP integration** — allows Ascent to detect live meeting context and activate the Cue Card overlay automatically
- **Google Calendar MCP** — surfaces upcoming high-stakes sessions (interviews, reviews, pitches) and pre-loads relevant coaching context before each conversation

