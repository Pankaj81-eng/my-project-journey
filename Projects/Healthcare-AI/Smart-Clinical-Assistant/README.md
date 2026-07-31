# Smart Clinical Triage

Built for a hackathon.

🎥 [Watch the demo](https://drive.google.com/file/d/1TgwwDbhPWnQ4IVDUnlfnAjwf6yeKrG87/view?usp=sharing)

## Business Problem

Clinical triage - working out what's wrong and how urgently a patient needs care - relies on a clinician's judgement applied against a huge space of possible conditions. Streamlining the intake and preliminary-diagnosis process, without ever letting AI make the final call, can cut time-to-treatment and reduce unnecessary referrals while keeping a clinician firmly in charge of every decision.

## Solution Overview

Smart Clinical Triage takes a patient's symptoms - via natural-language speech, uploaded images, or text - and runs them through a panel of specialty AI agents (Ortho, Cardio, Derma, and others) that debate a differential diagnosis: each proposes a candidate condition, critiques the others, and refines its position through multiple rounds. Each candidate diagnosis carries two confidence scores - an AI-based likelihood and an expert-informed likelihood - combined via a Naive Bayes approach, so clinical expertise captured in a knowledge graph directly shapes the AI's confidence, not just its raw output. A clinician reviews and approves every diagnosis before it goes further; an insurer review step and an appointments orchestrator (which books labs and doctor slots automatically) carry the approved plan through to action.

## Architecture

```
Patient (speech / image / text)
    |
Smart Clinical Triage Dashboard
    |
Specialty Agent Debate  --  Ortho / Cardio / Derma / ... agents
    |                       propose -> critique -> refine
    |
Knowledge Graph RAG DB  <--  Expert Knowledge Incorporation (clinician-extendable)
    |
Naive Bayes combination: AI-based likelihood + expert-based likelihood
    |
Clinician Review Dashboard  --  approve / feedback
    |
Insurance Review Dashboard  --  approve / feedback
    |
Appointments Orchestrator  -->  Lab booking
                            -->  Doctor / Clinic booking
```

1. **Multi-modal intake** - patients describe symptoms by speech, image upload, or free text, alongside structured details (location, demographics, vitals, medical history, allergies, insurance).
2. **Multi-agent debate** - specialty agents each propose a candidate diagnosis, critique each other's reasoning, and refine their position across rounds rather than voting once.
3. **Hybrid confidence scoring** - every candidate diagnosis carries an AI-based likelihood and a separate expert-based likelihood (sourced from a knowledge graph that clinicians can extend directly), combined via a Naive Bayes approach rather than trusting the LLM's confidence alone.
4. **Human-in-the-loop, twice over** - a clinician reviews and approves the diagnosis before an insurer review step also signs off, before anything reaches the appointments stage.
5. **Action, not just advice** - an Appointments Orchestrator turns an approved plan into real bookings: lab tests and doctor appointments, prioritised and filtered by location.

## Technologies Used

- Multi-agent debate architecture (propose / critique / refine)
- Knowledge Graph + RAG
- Naive Bayes (combining AI and expert-sourced likelihoods)
- LLM reasoning (diagnosis generation and appointment orchestration)
- Speech and image input processing
- Python

## AI Concepts Demonstrated

- Multi-agent debate for differential diagnosis, rather than a single model's one-shot answer
- Hybrid AI/expert confidence scoring - a principled way to let domain expertise correct model confidence
- Knowledge-graph-grounded reasoning that clinicians can directly extend
- Double human-in-the-loop review (clinician, then insurer) before any downstream action
- Explicit non-diagnostic framing - the tool surfaces a differential for a clinician to confirm, never a final diagnosis

## Key Learnings

- Multi-agent debate surfaces a better differential than a single model call - specialty agents catching each other's blind spots produces a more clinically useful shortlist than one model guessing alone.
- Blending AI-based and expert-based likelihoods (rather than picking one) gives a confidence score clinicians can actually trust, since it's visibly grounded in something beyond the model's own certainty.
- Going from "diagnosis" to "diagnosis with a booked appointment" - not stopping at advice - is what makes a triage tool actually useful rather than just informative.
- A clear, prominent safety disclaimer ("AI can make errors - consult an authorised medical professional for any final diagnosis") isn't boilerplate; it's core to how the tool should be used.

## Code

No public repo - a hackathon project documented through a demo video and presentation slides rather than published code.

## Future Enhancements

- Additional specialty agents beyond the current set
- Integration with EHR systems for patient-specific context (with appropriate access controls)
- Audit trail - every query, debate round, and approval logged for governance review
