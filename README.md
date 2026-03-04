# FraudGuard.ai

## Overview
FraudGuard AI is an **AI-powered scam awareness training platform** that simulates realistic phone scams in real time. Instead of reading about social engineering attacks, users experience them firsthand through a live phone call with an AI scammer.
The system uses conversational AI and voice synthesis to generate dynamic scam scenarios that respond to the user’s behavior. After the call ends, the conversation is analyzed and the user receives a **security awareness score** based on how safely they handled the interaction.
The goal of FraudGuard AI is to help people **recognize scam tactics and develop instincts to avoid real-world fraud attempts.**

## Features
### Real-time AI scam phone calls
Users receive a live phone call from an AI scammer that mimics common fraud tactics.

### Multiple scam scenarios
Examples include:
- Tech support scams
- Social Security impersonation
- Lottery or prize scams

### Dynamic AI conversations
The scammer responds in real time instead of following a fixed script.

### Live transcript streaming
The web dashboard shows a real-time transcript of the conversation.

### Automatic safety scoring
After the call, an AI model analyzes the transcript and assigns a **fraud awareness score** based on the user’s responses.

### Scenario-based training
Different scam agents simulate different types of social engineering attacks.

## How It Works
FraudGuard AI connects several services to create a real-time conversational phone experience.
1. The user enters their phone number on the website.
2. The backend triggers a call through Twilio.
3. The call audio is streamed through WebSockets.
4. User speech is transcribed and sent to an AI agent.
5. The AI generates responses and converts them to speech.
6. Audio is streamed back into the phone call.
7. The transcript is analyzed after the call to generate a safety score.

## System Architecture
FraudGuard AI is built around a real-time audio pipeline that connects a phone call to an AI conversational agent through streaming infrastructure.  

The system integrates telephony services, voice AI, and a web interface to create an interactive scam simulation environment.

### High-Level Architecture
```
User Phone
     │
     ▼
Twilio Programmable Voice
     │
     ▼
Twilio Media Streams (WebSocket)
     │
     ▼
FraudGuard Backend (Node.js / Express)
     │
     ├── Audio Transcoding (FFmpeg)
     │
     ├── Real-Time AI Conversation
     │      └── ElevenLabs Conversational Agents
     │
     ├── Transcript Streaming
     │      └── WebSocket → Browser UI
     │
     └── Conversation Scoring
            └── Groq / Llama Models
```
### Call Flow
**1. User starts a simulation**
The user enters their phone number and selects a scam scenario through the web interface.
**2. Backend initiates phone call**
The backend uses Twilio’s Programmable Voice API to place a call to the user.
**3. Twilio streams call audio**
Twilio Media Streams sends live audio to the backend through a WebSocket connection.
**4. Audio is transcoded**
The backend converts audio formats between telephony standards and AI model requirements using FFmpeg.
**5. AI generates responses**
The user's speech is sent to an ElevenLabs conversational agent which generates scammer responses in real time.
**6. AI speech is streamed back**
The generated speech is converted back to telephony audio format and streamed into the phone call.
**7. Transcript updates in real time**
Conversation transcripts are sent to the frontend dashboard through WebSockets.
**8. Call ends and scoring begins**
After the call ends, the transcript is analyzed by an LLM to generate a fraud awareness score based on the user's responses.

## Key Backend Components
### Session Manager  
Tracks active calls, transcripts, and scenario configurations.

### Audio Pipeline  
Handles bidirectional streaming between Twilio and the AI agent while converting audio formats.

### Scenario System  
Maps training scenarios to specific AI scam agents.

### Scoring Engine  
Uses an LLM to analyze transcripts and generate a safety score and explanation.

### WebSocket Gateway  
Streams transcripts and scoring results to the frontend dashboard.

## Real-Time Streaming Pipeline  
The most critical component of FraudGuard AI is the real-time audio bridge between the phone call and the AI agent.
```
User Speech
   ↓
Twilio Media Stream
   ↓
Backend WebSocket Server
   ↓
FFmpeg Audio Conversion
   ↓
ElevenLabs AI Agent
   ↓
Generated Speech
   ↓
FFmpeg Conversion
   ↓
Twilio Media Stream
   ↓
User Phone
```

This pipeline allows the system to maintain **low latency conversational interaction,** creating a realistic scam call experience.

## Tech Stack
Frontend
- React
- Vite
- WebSockets

Backend
- Node.js
- Express
- WebSocket server

AI / Voice
- ElevenLabs conversational agents
- Speech-to-text transcription
- AI-generated responses

Telephony
- Twilio Programmable Voice
- Twilio Media Streams

AI Analysis
- Groq API
- Llama 3 models

Infrastructure
- Cloudflare tunnels for local development

## Project Structure
```
fraudguard-ai  
│  
├── frontend  
│   ├── src  
│   └── package.json  
│  
├── backend  
│   ├── server.js  
│   └── package.json  
│  
├── dev-run.sh  
├── .env.example  
└── README.md
```

## Setup
### 1. Clone the Repository 
```
git clone https://github.com/quintuscarlson/fraudguard-ai.git  
cd fraudguard-ai  
```

### 2. Install dependencies
Backend  
```
cd backend  
npm install
```  

Frontend  
```cd ../frontend  
npm install
```

### 3. Create environment variables
Create a `.env` file in the project root.  
Example:  
```
TWILIO_ACCOUNT_SID=  
TWILIO_AUTH_TOKEN=  
TWILIO_PHONE_NUMBER=  

ELEVENLABS_API_KEY=  
ELEVEN_AGENT_ID_LOTTERY=  
ELEVEN_AGENT_ID_TECH=  
ELEVEN_AGENT_ID_SOCIAL=  

GROQ_API_KEY=  

BASE_URL=  
WSS_URL=  
PORT=3000
```  

### 4. Start the development environment
From the project root:    
```
./dev-run.sh
```  

This will:  
- Start a Cloudflare tunnel  
- Launch the backend server
- Provide public URLs required for Twilio

Then start the frontend:  
```
npm run dev
```  
Open the web interface:  
```
http://localhost:5173
```

## Example Workflow
1. User enters their phone number
2. User selects a scam scenario
3. The system calls the user
4. A live AI scam conversation occurs
5. The transcript appears on the dashboard
6. The system generates a fraud awareness score

## Security Notice
FraudGuard AI is designed **only for educational and cybersecurity training purposes.**
The system simulates scam tactics to help users recognize social engineering attacks and improve personal security awareness.
It should not be used for deceptive or malicious activity.

## Future Improvements
- Additional scam scenarios
- Real-time scam tactic detection
- Adaptive difficulty levels
- Analytics dashboards for training programs
- Enterprise cybersecurity training integrations

## Project Origin
FraudGuard AI was originally developed during a hackathon as part of a team project focused on improving public awareness of phone scams and social engineering attacks.  

During the hackathon, our team explored the idea of simulating realistic scam phone calls as a training tool. I was responsible for the majority of the system implementation, including the backend architecture, real-time audio streaming pipeline, AI integration, and scoring system.  

The current version expands significantly on the original prototype and focuses on creating a fully interactive training experience powered by conversational AI.

## License
MIT License
