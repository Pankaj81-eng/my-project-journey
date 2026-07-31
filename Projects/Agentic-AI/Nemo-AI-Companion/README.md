# Nemo - AI Hospital Companion

## Business Problem

Hospitalised patients spend long stretches of time with medical questions, anxiety, and boredom that nursing staff can't always address immediately. A voice-first companion that can answer routine medical questions, offer emotional support, and provide light entertainment - while staying clearly non-diagnostic - reduces that gap without adding to clinical workload.

## Solution Overview

Nemo is a multi-agent AI hospital companion built with CrewAI. A coordinator agent ("Nemo") greets the patient and routes each request to one of three specialists - Medical, Wellbeing, or Recreation - based on what's being asked. The whole interaction is voice-first: patients speak naturally, and Nemo responds in kind.

## Architecture

```
Patient (voice)
    |
Web Speech API (speech-to-text)
    |
Next.js frontend  -->  FastAPI backend
    |
CrewAI Coordinator ("Nemo") -- routes to -->  Medical Agent
                                          -->  Wellbeing Agent
                                          -->  Recreation Agent
    |
Azure OpenAI GPT-4o (agent reasoning)
    |
Azure Neural TTS (voice response)
```

## Technologies Used

- CrewAI (multi-agent coordination)
- LangChain
- Azure OpenAI GPT-4o
- Azure Speech Services (speech-to-text + neural text-to-speech)
- Next.js 14 + TypeScript (frontend)
- FastAPI (backend)
- Web Audio API (live audio visualisation)

## AI Concepts Demonstrated

- Multi-agent coordination with delegation (a coordinator agent routing to specialist agents, not a single monolithic prompt)
- Domain-differentiated agent personalities - each specialist has its own role, temperature, and token budget suited to its task
- Voice-first interaction design, not text-first with voice bolted on
- Non-diagnostic-by-design scope for a healthcare-adjacent assistant - the Medical agent explains, it doesn't diagnose

## Key Learnings

- Giving each specialist agent a distinct temperature (Medical at 0.3 for accuracy, Recreation at 0.7 for playfulness) produced noticeably more appropriate responses than a single shared setting across all agents.
- A coordinator agent with delegation enabled while specialists have it off keeps routing logic centralised and predictable - only one agent decides where a request goes.
- For a healthcare-adjacent voice product, scoping the Medical agent to explain rather than diagnose from the start avoided a whole category of safety and trust problems later.

## Code

Private repo - a hackathon project built with a small team. Kept private rather than public.

## Future Enhancements

- Multi-language support for diverse patient populations
- EHR integration for personalised medical information (with appropriate access controls)
- Additional specialist agents (nutrition, pharmacy, discharge planning)
- Analytics dashboard for conversation insights and patient sentiment
