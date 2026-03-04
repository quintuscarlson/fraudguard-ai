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
- 
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
