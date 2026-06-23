# Python Mentor

## Business Problem

Learning to code is hard because feedback is delayed. Beginners write code, run it, get an error, and don't know why. Traditional courses explain concepts but can't respond to what a specific learner got wrong in their specific submission. An AI-powered mentor can give immediate, personalised, and educational feedback on every attempt.

## Solution Overview

TechTales Python Mentor is an interactive Python learning platform built with Streamlit. Learners progress through structured lessons (Variables, Data Types, If/Else, Loops, Functions), write code in a sandboxed editor, and receive immediate per-requirement feedback. XP and progress tracking provide light gamification. The platform is designed for absolute beginners — every piece of feedback is written to be readable by someone who has never programmed.

## Architecture

```
Streamlit UI (app.py)
    ↓
Sandboxed Code Execution (subprocess + 2s timeout + AST validation)
    ↓
AST-Based Validator (per-topic, per-requirement checks)
    ↓
SQLite (progress, XP, completions)
    ↓
Feedback Panel (per-requirement pass/fail + improvement suggestions)
```

1. **Sandboxed Execution** — learner code is validated with AST analysis before running, then executed in an isolated subprocess with a 2-second timeout and a restricted builtin allowlist. No imports, globals, or file access.
2. **Per-Topic Validators** — each lesson has a dedicated validator that checks specific requirements (e.g., "used a for loop", "defined a function with a parameter"). Requirements return pass/fail + a plain-English suggestion when failing.
3. **Progress Tracking** — SQLite records lesson views, challenge completions, and XP (20 XP on first pass per topic). Progress states: Not Started → Lesson Viewed → Completed.
4. **Topic Gating** — later topics are locked until earlier challenges are passed, ensuring foundational concepts are in place.

## Technologies Used

- Python 3.9
- Streamlit (UI and routing)
- SQLite (progress and XP storage)
- AST module (code validation and security)
- Claude API (planned — AI mentor for question answering)

## AI Concepts Demonstrated

- AI Learning Assistant (personalised, adaptive feedback)
- Interactive Learning (real-time code execution and feedback)
- Python Education (structured curriculum with progressive complexity)
- Personalized Guidance (per-requirement feedback, not generic pass/fail)

## Key Learnings

- AST-based validation is more reliable than output matching for beginners — it checks whether they used the right construct, not just whether they got the right answer.
- Subprocess isolation is essential for educational sandboxes — learner code must not be able to affect the host process.
- Per-requirement feedback (not a single pass/fail) dramatically improves the learning experience — learners know exactly what to fix.
- Gamification (XP, progress states) increases completion rates even for simple systems.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- AI Mentor mode — ask questions about the current lesson, get explanations for mistakes (Claude API integration planned)
- Voice learning — listen to lessons and respond verbally
- Daily challenges — new coding problems each day with a streak tracker
- Full AST validators for Data Types, If/Else, and Functions (currently generic)
