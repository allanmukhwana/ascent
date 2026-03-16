##  Inspiration

Most career advice arrives too late.

You finish a job interview, a performance review, or a board presentation. Days pass. A rejection lands. You're told you "lacked executive presence" or "didn't demonstrate leadership." You'll never know what specific moment cost you the opportunity — or what you could have said instead.

We kept asking the same question: why do sales teams get real-time, data-driven intelligence on every conversation they have, while everyone else navigating their careers does it completely blind?

The answer wasn't a lack of technology. The Gemini Live API changes everything — for the first time, an AI can listen, understand context, and surface guidance fast enough to actually change the outcome of a live conversation. We built Ascent to put that capability in the hands of every professional on earth, from a student preparing for their first interview to an executive addressing a board.

The insight that drove us: *career advancement is not a knowledge problem. It's a behavioral awareness problem.* People don't fail because they don't know what to say. They fail because nobody is watching, measuring, and coaching them in the moments that matter.

---

##  What It Does

Ascent is a **Human Potential Intelligence platform** — a live AI agent that transforms professional conversations into measurable career data.

**Four core capabilities:**

**1. Live Cue Cards** — The centerpiece of the Gemini Live API integration. During any live video call (interview, 1:1, performance review, pitch), Ascent runs a minimal on-screen overlay invisible to the other party. The agent listens to both sides of the conversation simultaneously, analyzes what's happening in under 200ms, and surfaces whispered micro-coaching in real time: *"You've spoken 74% of this conversation — pause and ask an open question."* or *"Defensive tone detected — reframe with what you learned."* Cue Cards are contextual, timing-specific, and calibrated to each user's known behavioral weaknesses.

**2. Conversation Intelligence Scorecards** — After every session, Ascent generates a structured behavioral scorecard across 14 dimensions: talk-to-listen ratio, filler word frequency, impact vocabulary usage, storytelling structure (STAR compliance), leadership language gradient, emotional intelligence signals, and more. Each score is benchmarked against a Career Stage Playbook — students are measured against top-quartile recruiting benchmarks, managers against director-level presence standards.

**3. The Advancement Deal Board** — Ascent treats career goals as managed pipelines. A user creates an Advancement Deal (e.g., "Promotion to Senior PM in 9 months") and Ascent actively tracks its health: behavioral trajectory vs. required benchmarks, active risk alerts, milestone completion, and a "Next Best Action" ranked by impact. It answers the question no performance review answers honestly: *"Am I actually on track?"*

**4. Career Stage Framework** — The same platform intelligently serves a 19-year-old student and a 52-year-old CEO because its benchmarks, metrics, and coaching language adapt completely based on career stage — Student, Entry-Level, Mid-Manager, Senior Leader, and Executive.

---

##  How We Built It

**Frontend:** Vanilla HTML5, CSS3, and JavaScript — no frontend framework. We chose this deliberately: maximum performance, zero build toolchain complexity, and complete control over the WebSocket integration required for Gemini Live API streaming. The Cue Card overlay is a carefully engineered floating HUD built in pure CSS/JS that renders on top of any video call without interfering with the meeting window.

**Backend:** PHP (vanilla, no framework) handles all REST API endpoints, session management, authentication, webhook routing, and the orchestration layer between the frontend and Google's APIs. PHP processes incoming Gemini Live API events and manages the dual-agent pipeline.

**Database:** MySQL stores all structured application data — user profiles, career stage configurations, Advancement Deals, milestone records, session metadata, and benchmark configurations. Designed with a multi-tenant schema ready for enterprise team deployments.

**Google Technologies:**
- **Gemini Live API** — the core of the Live Cue Card system. Bidirectional audio streaming, real-time transcription, and behavioral analysis at sub-200ms latency
- **Agent Development Kit (ADK)** — orchestrates two specialized agents: the Live Session Agent (Cue Cards) and the Career Intelligence Agent (Scorecards + Deal Board health analysis)
- **Vertex AI** — hosts the behavioral benchmark models used to score sessions against career-stage-specific playbook standards
- **Cloud Firestore** — stores session transcripts, behavioral analysis results, personal coaching history, and the data that trains the personal playbook over time
- **Cloud Storage** — archives session audio for Highlight Reel and Danger Moment playback in scorecards
- **Cloud Run** — containerized deployment of the PHP backend and WebSocket server with auto-scaling
- **Google Meet MCP integration** — allows Ascent to detect live meeting context and activate the Cue Card overlay automatically
- **Google Calendar MCP** — surfaces upcoming high-stakes sessions (interviews, reviews, pitches) and pre-loads relevant coaching context before each conversation

---

##  Challenges We Ran Into

**Latency vs. usefulness in a live conversation.** Real-time coaching only works if it arrives before the moment passes. Getting the full pipeline — audio capture → Gemini Live API transcription → behavioral analysis → Cue Card render — under 300ms end-to-end required significant WebSocket architecture work and careful prompt engineering to keep the ADK agent responses concise enough to be glanceable in under a second.

**Avoiding cognitive overload.** Early prototypes showed Cue Cards firing too frequently, making users feel more anxious, not less. We had to build a suppression system that weighs urgency, recency of the last cue, and conversation pace before surfacing a prompt. The agent learned to stay silent in moments of genuine flow.

**Calibrating benchmarks without proprietary training data.** Building career-stage benchmark playbooks without access to thousands of real recorded professional conversations required a grounded methodology — we used NACE Career Readiness Competencies, published research on executive communication patterns, and validated interview frameworks as the foundation, then layered Gemini's reasoning to contextualize scoring.

**PHP WebSocket architecture for streaming.** PHP is not the natural home for long-lived streaming connections. We built a lightweight WebSocket server layer using Ratchet that bridges the Gemini Live API audio stream with the frontend overlay, managing connection state, reconnection logic, and graceful degradation when audio quality drops.

---

##  Accomplishments We're Proud Of

**The Cue Card system works as imagined.** Seeing it fire the right coaching prompt at exactly the right moment — mid-sentence, before the user has finished the mistake — during a live mock session was the validation moment the entire team needed.

**14-dimension behavioral analysis from a single audio stream.** Extracting talk ratio, sentiment, leadership language gradient, STAR compliance, impact vocabulary usage, and eight other signals from a live conversation — and doing it in a way that's explainable and actionable, not just a number — is technically and intellectually the work we're most proud of.

**A career framework that spans 40 years of professional life.** Building a single platform that meaningfully serves a student rehearsing their first job interview and a founder preparing a Series B pitch — with completely different benchmarks, metrics, and coaching language for each — required deep thinking about what "performance" means at every career stage.

**Clean architecture with minimal dependencies.** The entire platform runs on PHP, MySQL, HTML, and JS. No npm, no framework overhead, no build step. It's fast, portable, and deployable anywhere — which matters enormously for the emerging market users we're designing for.

---

##  What We Learned

**Behavioral coaching is fundamentally different from informational advice.** We learned that users don't need to be told *what* to say in career conversations. They need to be shown, in real time, *how* they're actually showing up — and given a single, specific, immediately actionable adjustment. The most effective Cue Cards are never longer than 12 words.

**The data is in the pattern, not the session.** A single scorecard tells you little. Ten scorecards tell you exactly where your career ceiling is. The longitudinal behavioral graph — watching the same person improve, plateau, and break through a specific weakness — is where the real intelligence lives.

**Latency is a product decision, not just a technical one.** Every 50ms we shaved off the pipeline changed how the Cue Card felt. Under 200ms feels like intuition. Over 400ms feels like interruption. The acceptable window for real-time coaching is narrower than we expected — and getting inside it required rethinking the entire event handling chain.

**People are remarkably honest when they're being analyzed, not judged.** Test users opened up about their deepest professional insecurities — fear of sounding stupid in senior meetings, history of talking too much under pressure, chronic inability to quantify impact — once they understood Ascent was a mirror, not a critic.

---

##  What's Next for Ascent

**Multimodal expansion — video and body language.** The next version integrates Gemini's vision capabilities to analyze eye contact, posture, and facial expression in video calls — adding a non-verbal intelligence layer to the existing audio analysis.

**Ascent for Teams.** An enterprise dashboard where managers can review their team's collective coaching data, identify shared weaknesses, and design targeted development sprints — replacing expensive external coaching programs with measurable, continuous in-the-flow intelligence.

**The Career Intelligence API.** Opening Ascent's benchmark and scoring engine as an API — allowing universities, recruiting platforms, HR software vendors, and professional certification bodies to embed behavioral career intelligence into their own products.

**Afya track — Emerging market expansion.** Localizing the Career Stage Framework for high-growth professional markets in Africa, Southeast Asia, and Latin America — where the fastest-growing professional populations have the least access to quality career coaching infrastructure. This means Swahili, Bahasa, and Portuguese language support with region-specific benchmark calibration.

**Google Workspace native integration.** A first-party integration that activates Ascent's Live Cue Card system directly inside Google Meet — making behavioral career coaching a native feature of the world's most widely used professional collaboration platform.

