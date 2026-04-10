# System Architecture: AI Pet Mental Health Analyzer 🐾🧠

This document outlines the architecture and implementation strategy for building a gamified application that passively analyzes mental health through pet care interactions and conversational analysis.

## 🏗️ Core Technology Stack

1. **Frontend / Game Engine: React + Three.js (React Three Fiber)**
   - **Why?** Since you are animating in **Blender**, exporting your models and animations to `GLTF/GLB` formats and rendering them using Three.js in a web browser is the most accessible and modern approach. It allows users to play instantly on any device.
   - **Framework:** Next.js or Vite.
   - **Styling:** CSS/Tailwind for a premium, dynamic, and soothing UI.

2. **The "Brain": Google Gemini 1.5 Pro**
   - **Why?** Gemini 1.5 Pro has a massive context window, perfect for tracking long-term behavior and chat logs, allowing it to accurately detect subtle changes in a user's tone or sentiment over time.
   - **Usage:** Gemini will act as both the conversational AI driving the pet's dialogue and the analytical engine evaluating the user's mental state.

3. **Backend & Monitoring: Firebase**
   - **Authentication:** Firebase Auth to track individual users.
   - **Database:** Cloud Firestore to store:
     - Player interaction metrics (feeding times, play frequency).
     - Chat histories.
     - Ongoing mental health evaluation scores.
   - **Serverless Compute:** Firebase Cloud Functions or a lightweight Node.js server to securely handle Gemini API calls (to keep API keys secure).

---

## ⚙️ How the Analysis Works (The Core Loop)

The app determines the user's mental state using two primary passive streams:

### 1. Behavioral Analysis (How they treat the pet)
The game tracks quantitative metrics about the player's responsibility and interaction.
- **Metrics Tracked:** 
  - Login frequency (are they lethargic/withdrawn or obsessive?)
  - Time taken to respond to pet's needs (feeding, cleaning, healing).
  - Types of items chosen for the pet (e.g., healthy food vs. junk food, high-energy play vs. low-energy play).
- **The Process:** These metrics are logged to **Firebase**. Periodically, an aggregated summary of this behavior is sent to **Gemini 1.5 Pro** behind the scenes: 
  *Prompt Example:* "The user has logged in 50% less this week and ignored the pet's hunger for 12 hours twice. Analyze what this behavioral change might indicate..."

### 2. Conversational Analysis (How they speak to the pet)
The user can chat directly with the pet.
- **The Process:** The pet responds using Gemini, staying in character as a supportive, empathetic companion. 
- **Tone Detection:** While generating the pet's response, we use Gemini's structured JSON output to simultaneously return a private "mental state assessment" of the user's input, analyzing:
  - Sentiment (Positive, negative, neutral)
  - Stress indicators (Word choice, urgency, self-deprecating remarks)
  - Emotional volatility.

### 3. The Monitor Dashboard
A private dashboard (potentially for a counselor, parent, or just raw data charts for the user) pulls data from **Firestore** to visualize long-term trends in the user's mental health score.

---

## 🚀 Implementation Roadmap

### Phase 1: Foundation & The 3D Environment (Days 1-2)
- Set up a React/Vite project.
- Integrate **Firebase** (Auth and Firestore).
- Implement **React Three Fiber**.
- Load a simple placeholder 3D model exported from **Blender** and trigger a basic idle/happy animation.

### Phase 2: The Core Game Mechanics (Days 2-3)
- Build the UI: Health bars, Hunger meters, and interaction buttons (Feed, Play).
- Write logic to decrease pet stats over time.
- Connect actions to Firestore to log timestamps of user behaviors.

### Phase 3: The Gemini "Brain" Integration (Days 3-4)
- Create a secure Node.js endpoint or Firebase Cloud Function.
- Build the Chat UI so the user can talk to the pet.
- Connect the chat to the Gemini 1.5 Pro API.
- Prompt engineer Gemini to embody the pet persona.

### Phase 4: The Mental Health Analyzer Engine (Days 4-5)
- Write the scheduled "analysis prompt" that takes the week's Firebase logs and chat history, feeds it to Gemini, and extracts a mental health score.
- Build a simple dashboard/graph to display the monitoring results based on Firestore data.

---

## Next Steps

To get started, we should initialize the web application and set up the foundation for loading your Blender models and connecting to Firebase. 

Would you like me to initialize a modern React project (using Vite) right now in this folder?
