🇮🇳 AI Note Taker: Indic-First YouTube Learning Extension
Bridging the Educational Language Gap with Multimodal AI

AI Note Taker is a conceptualized Chrome extension designed for the AI for Bharat 2026 Hackathon. It addresses the challenge of making high-quality YouTube educational content accessible to learners across India by providing automated, localized notes and quizzes in 11+ Indic languages.
🎯 The Vision

Most educational content on YouTube is in English or high-level Hindi. For students who prefer learning in their mother tongue—be it Tamil, Telugu, Marathi, or Bengali—language becomes a barrier to comprehension.

Our project leverages Google Gemini 2.0 Flash to not just transcribe, but visually and auditorily understand video content, translating complex concepts into structured study tools in the user's native language.
🛠️ Project Workflow (The "Spec-Driven" Approach)

This repository currently contains the core Technical Specifications and Requirement Framework for the project, following a rigorous development workflow:
1. Requirement Engineering (requirements.md)

    YouTube Tab Capture: Automatic detection of educational content and metadata extraction.

    Multilingual Summarization: Support for 10+ Indic languages with a "Hindi-first" priority.

    Smart Quiz Generation: AI-generated MCQs (5 per video) designed to test depth of understanding.

    Data Ethics: A strict "Zero-Tracking" policy and safety filters to ensure a secure learning environment.

2. Architectural Design (design.md)

    Three-Tier Architecture: A React frontend, Node.js backend, and the Google Gemini API.

    Multimodal Processing: Instead of simple text transcripts, the system uses the Google AI File API to analyze video frames and audio cues.

    Hybrid Language Handling: Specifically designed to handle "Hinglish" and code-switched audio common in Indian classrooms.

    Performance Optimization: 1-hour TTL (Time-To-Live) caching and local storage for offline note access.

🏗️ Tech Stack (Proposed)

    AI Engine: Google Gemini 2.0 Flash (Multimodal)

    Frontend: React + Tailwind CSS (Manifest V3)

    Backend: Express.js on Google Cloud Run

    Language Support: Hindi, Tamil, Marathi, Telugu, Bengali, Gujarati, Kannada, Malayalam, Punjabi, Odia, and English.

📂 Repository Contents

    requirements.md: Detailed User Stories and Acceptance Criteria using EARS notation.

    design.md: Technical blueprints, Mermaid diagrams, and TypeScript data models.

🤝 AI for Bharat 2026

This project is dedicated to the AI for Learning theme, aiming to democratize access to education for 1.4 billion people through the power of Generative AI.
