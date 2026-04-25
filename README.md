# DemocrAI

DemocrAI is an intelligent, user-centric web application designed to demystify the democratic process. By combining a guided, step-by-step UI with an integrated AI assistant powered by Google Gemini, DemocrAI empowers citizens to navigate voter registration, election timelines, and civic duties with absolute clarity.

---

## 🏛️ Chosen Vertical

**Civic Technology & Election Guidance**

Navigating the election process can be overwhelming for first-time voters and experienced citizens alike. Changing deadlines, complex registration requirements, and a lack of accessible, conversational guidance often lead to voter drop-off. DemocrAI tackles this vertical by providing a streamlined, accessible, and AI-augmented platform that acts as a personal civic guide.

---

## 🧠 Approach and Logic

Our core philosophy is **Clarity through Structure and Conversation**.

1.  **Structured Guidance**: We break down the complex election cycle into digestible, actionable steps (e.g., Registering to Vote, Researching Candidates, Voting on Election Day). This linear progression is enforced by a locked-step UI, ensuring users don't skip critical prerequisites.
2.  **Conversational AI Support**: Recognizing that static FAQs cannot cover every edge case (e.g., "What if I recently moved?"), we integrated an AI assistant directly into the interface. This provides users with instant, contextual answers without forcing them to leave the platform.
3.  **Resilience and Performance**: We prioritized a premium user experience. The app is built to be fast (60fps React rendering), accessible (full screen-reader support), and resilient against network failures (smart Firestore fallbacks).

---

## ⚙️ How the Solution Works

### The Architecture
DemocrAI is a modern Single Page Application (SPA) built with **React** and **Vite**, styled with **Tailwind CSS**. 

### Key Features
*   **Interactive Step Guide (`StepGuide.jsx`)**: A central timeline of actionable cards. Users must mark preceding steps as "Done" before unlocking the next, ensuring a logical flow.
*   **Live Election Timeline (`Timeline.jsx`)**: Displays critical upcoming dates. It attempts to fetch real-time data from **Firebase Firestore** but seamlessly falls back to static data if the network or an ad-blocker interferes.
*   **DemocrAI Assistant (`ChatAssistant.jsx`)**: A sticky, chat-based interface powered by the **Google Gemini 2.5 Flash API**. It features a dynamic typing effect, pre-populated suggestion chips, and robust XSS sanitization (`sanitizeInput`).
*   **Progress Tracking**: A dynamic top banner tracks the user's progress through the election cycle, providing a sense of accomplishment.

### Security & Accessibility
*   **Security Headers**: The app enforces strict Content Security Policies (CSP), Referrer Policies, and MIME-sniffing protections to prevent XSS and data leakage.
*   **a11y**: Features invisible `aria-live` regions to announce AI typing updates to screen readers, ensuring the dynamic UI remains completely accessible.

---

## 📌 Assumptions Made

During development, several key assumptions were made to scope the solution effectively:

1.  **Generalized Election Data**: We assume a generalized federal/national election timeline. Local or state-specific nuances (which vary wildly) are intended to be handled by the AI assistant answering specific user queries, rather than hardcoded into the UI steps.
2.  **Firebase Limitations**: We assume that in some environments, aggressive browser tracking protections or ad-blockers might block Firebase Analytics or Firestore connections. Therefore, the app is designed to function 100% locally with static fallback data if the database is unreachable.
3.  **Stateless Sessions**: For this iteration, user progress (completed steps) and chat history are managed in local React state. We assume the user completes their session in a single browser sitting. Persistent user accounts and cross-device sync are scoped for future versions.
4.  **AI Hallucination Mitigation**: We assume the Gemini model is robust enough to handle general civic queries, but the user is ultimately responsible for verifying critical deadlines with official local government sources.
