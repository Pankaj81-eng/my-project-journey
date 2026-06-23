# Voice Pizza Agent

## Business Problem

Telephone-based ordering systems are costly to staff, slow at peak times, and deliver inconsistent customer experiences. A voice AI agent can handle the full ordering conversation — taking the order, handling modifications, confirming details, and managing payment handoff — without queue times or training costs.

## Solution Overview

A real-time voice agent that conducts a natural, multi-turn conversation with customers to take pizza orders. Built on OpenAI Realtime APIs for low-latency voice interaction, with an agentic workflow managing order state, item validation, upsell prompts, and confirmation. The agent maintains full conversation context across turns and gracefully handles corrections and ambiguous requests.

## Architecture

```
Customer (voice input)
    ↓
OpenAI Realtime API (speech-to-text + LLM + text-to-speech)
    ↓
Agentic Order Manager (tool-use loop)
├── Menu Lookup Tool
├── Order State Manager
├── Upsell Tool
└── Confirmation + Handoff Tool
    ↓
Order System (webhook / API)
```

1. **Voice Interface** — OpenAI Realtime APIs handle speech-to-text and text-to-speech in a single low-latency pipeline, enabling natural conversation without perceptible delay.
2. **Agentic Order Manager** — an LLM-driven agent maintains order state across turns, calling tools to look up menu items, add or remove items, and validate the order before confirmation.
3. **Multi-turn Dialogue** — the agent tracks conversation history, handles corrections ("actually, make that a large"), and disambiguates unclear requests ("which size?").
4. **Handoff** — once confirmed, the order is submitted via webhook to the order management system and the agent confirms with a reference number.

## Technologies Used

- OpenAI Realtime APIs (voice + LLM)
- Python (agent orchestration)
- WebSockets (real-time audio streaming)
- FastAPI (webhook and API layer)

## AI Concepts Demonstrated

- Voice AI (real-time speech interaction)
- Agentic Workflows (tool-use loop for order management)
- Order Management (stateful, multi-step ordering)
- Multi-turn Conversations (context preservation across turns)

## Key Learnings

- Low-latency is critical for voice — any perceivable pause breaks the conversational feel. OpenAI Realtime APIs handle this at the API level, removing the need to chain separate ASR → LLM → TTS calls.
- Stateful order management via tool use is more reliable than trying to maintain order state in the LLM context alone — tools act as the ground truth.
- Handling corrections mid-conversation requires explicit state tracking, not just re-reading the transcript.
- Graceful failure (item not available, unclear request) needs explicit agent paths — the LLM alone will hallucinate menu items if not grounded in a real lookup tool.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- Support for loyalty programme lookup (recognise returning customers by phone number)
- Multi-language support using Realtime API language switching
- Live order tracking integration — agent can answer "where's my order?" questions
- Sentiment detection — escalate to human agent if customer frustration is detected
