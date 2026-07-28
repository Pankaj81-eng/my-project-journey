# Voice Pizza Agent

🎥 [Watch the demo](https://www.youtube.com/watch?v=KLMR7H7rU3g)

## Business Problem

Ordering food by voice sounds simple until you look at what actually has to happen between "get me a pizza" and a completed order: understanding intent, matching it to a real menu within budget, and then acting on it - without silently placing an order the user didn't confirm.

## Solution Overview

A voice-first pizza ordering agent with a three-layer pipeline. The **brain layer** uses LangChain with Google Gemini (structured JSON output) to extract order intent from natural speech or text. The **decision layer** matches that intent against a menu catalogue, validates it against budget, and selects a store. The **automation layer** uses Playwright to drive a real checkout flow through to the final step - and stops there. A human always confirms before anything is submitted.

## Architecture

```
Voice / text input (Web Speech API)
    |
LangChain + Gemini 2.5 Flash  --  structured OrderIntent (JSON schema)
    |
Decision layer  --  menu match, budget check, store selection  -->  OrderPlan
    |
Playwright automation  --  fills checkout, pauses before final submit
    |
Human confirmation  -->  order placed
```

## Technologies Used

- React 19, TypeScript, Vite
- Express (Node.js backend)
- LangChain + Google Gemini (structured output)
- Playwright (Chromium automation)
- Zod (schema validation)

## AI Concepts Demonstrated

- Structured output extraction (JSON schema-constrained generation, not free text)
- A decision layer that keeps business logic - budget, matching - out of the LLM and in deterministic code
- Human-in-the-loop guardrails around an agent that can take real-world action
- Voice as an input modality on top of an otherwise text-first pipeline

## Key Learnings

- Separating "what does the user want" (LLM) from "is this a valid, affordable option" (deterministic code) makes the system far easier to test and debug than asking the LLM to do both.
- Browser automation against a real site is fragile by nature - selector strategies need multiple fallbacks, and the automation should always have a safe stopping point rather than assuming every click succeeds.
- A human-in-the-loop pause isn't just a safety feature, it's what makes it reasonable to automate a real transaction at all.

## Code

This is a personal project with real, working automation against live pizza ordering sites. The repository stays **private** rather than public - the code targets specific third-party sites by name, and publishing automation against a live business's checkout without their agreement isn't something to hand out, even with the safety guardrail in place.

A [demo video](https://www.youtube.com/watch?v=KLMR7H7rU3g) shows the full flow end-to-end.

## Future Enhancements

- Additional store adapters behind the same decision-layer interface
- Persisted order history and repeat-order shortcuts
- Multi-language voice input
