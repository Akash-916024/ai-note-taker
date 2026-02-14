# AI Note Taker – Indic-First Browser Extension 🇮🇳🤖

## Overview

**AI Note Taker** is an AI-powered browser extension designed for the **AI for Bharat Hackathon**.  
It helps students and learners convert long educational **YouTube videos into concise study notes and quizzes**, with **first-class support for Indian (Indic) languages**.

The project focuses on **accessibility, multilingual learning, privacy, and efficiency**, making quality educational content easier to understand and revise for learners across India.

---

## Problem Statement

Students in India often depend on long-form educational videos but face challenges such as:
- Difficulty extracting key points from lengthy lectures
- Limited support for Indian regional languages
- Lack of quick revision materials
- No way to ask contextual questions based on video content

Existing tools are often English-centric, heavy, or unsuitable for low-resource environments.

---

## Proposed Solution

AI Note Taker is a **lightweight Chrome extension** that:
- Automatically captures the currently playing YouTube video
- Generates **structured summaries** using AI
- Creates **interactive quizzes** for self-assessment
- Supports **multiple Indic languages**
- Works efficiently even on low-end devices

The system uses **Google Gemini’s multimodal AI capabilities** to understand video content and deliver accurate educational outputs.

---

## Key Features

- 📹 **Automatic YouTube Video Detection**
- 📝 **AI-Based Video Summarization**
- ❓ **Smart Quiz Generation (5 MCQs per video)**
- 🌐 **Multilingual Support (Indic-first)**
  - English, Hindi, Tamil, Telugu, Malayalam, Marathi, Bengali, Gujarati, Kannada, Punjabi, Odia
- 💾 **Local History & Caching**
- 🌙 **Dark / Light Theme Support**
- 🔒 **Privacy-First Design (No Tracking, No Login)**

---

## Architecture Overview

The system follows a **three-tier architecture**:

1. **Frontend**  
   - Chrome Extension (Manifest V3)
   - React + Tailwind CSS

2. **Backend**  
   - Node.js + Express
   - Hosted on Google Cloud Run / Firebase

3. **AI Services**
   - Google Gemini 2.0 Flash API
   - YouTube Data API v3

Detailed architecture, data flow, and component design are documented in `design.md`.

---

## AI for Bharat Alignment

This project aligns strongly with **AI for Bharat goals** by:

- 🇮🇳 Supporting **Indian regional languages**
- 📚 Focusing on **education and learning**
- 🧠 Using **responsible AI practices**
- ⚡ Designing for **low-bandwidth and low-resource environments**
- 🔓 Being **open-source friendly**

---

## Repository Contents

---

## How the System Works (High Level)

1. User opens a YouTube video
2. User clicks the extension icon
3. The extension captures the video URL
4. Backend sends the video to Gemini AI for processing
5. AI generates:
   - A structured summary
   - A quiz with explanations
6. Output is displayed in the selected Indic language
7. Results are cached locally for fast access

---

## Privacy & Responsible AI

- No user login required
- No tracking or analytics without consent
- No storage of personal user data
- Temporary AI processing files are deleted after use
- AI safety filters are enabled to block harmful content

---

## Future Enhancements

- Offline access to saved summaries
- Export notes as PDF or Markdown
- Timestamp-based navigation
- Voice-based summaries
- Support for additional platforms beyond YouTube
- Firefox and Edge browser support

---

## Hackathon Information

- **Event**: AI for Bharat Hackathon
- **Submission Includes**:
  - `requirements.md` (Generated via Kiro – Spec)
  - `design.md` (Generated via Kiro – Design)
  - Presentation deck (submitted separately)

---

## Team

Developed as part of the **AI for Bharat Hackathon**  
Focused on building inclusive, AI-powered educational tools for India 🇮🇳

---
