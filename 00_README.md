
# AI System Design Prompting Framework

## Overview

This repository provides a **structured prompting workflow** for designing production-grade software systems with AI agents.

It is based on a simple premise:

> AI produces dramatically better systems when given structure, guardrails, and sequencing.

Most AI-driven projects fail not because the models are weak — but because the **process is improvisational**.

This framework replaces improvisation with a **repeatable, artifact-driven design pipeline**.

---

## Why This Exists

When building software with AI, the most common failure modes are:

- Starting with the tech stack too early  
- Letting the AI invent architecture  
- Skipping business context  
- Over-engineering infrastructure  
- Producing inconsistent documentation  
- Allowing design entropy  
- Jumping straight into code  

This framework prevents those mistakes by forcing a **deliberate design phase** before implementation.

Think of it as:

> Product thinking → System design → Execution structure → Code

Not the other way around.

---

## Core Philosophy

### 1. Sequence Creates Quality
Good systems are rarely accidents.  
The order of decisions matters.

### 2. Calm Systems Win
Prefer simplicity that will still feel correct in 5–10 years.

### 3. Boring Scales
Innovation belongs in the product — not the infrastructure.

### 4. Decisions Must Be Captured
Undocumented decisions are eventually undone.

### 5. Control the AI Environment
AI agents behave according to the constraints you provide.

---

## How the Framework Works

Each template represents a **distinct design phase**.

You do NOT run them all at once.

Instead, you:

1. Tag a step (or paste the template).
2. Let the AI lead an interactive discovery session.
3. Iterate until both parties are satisfied.
4. Produce the artifact.
5. Move to the next step.

This creates a **human ↔ AI design loop**.

---

## Workflow

Run the steps **in order**:

1. `@AI-STEP-01` — Business Context  
2. `@AI-STEP-02` — PRD  
3. `@AI-STEP-03` — Assumption Stress Test  
4. `@AI-STEP-04` — Decision Log  
5. `@AI-STEP-05` — Architecture & Data Model  
6. `@AI-STEP-06` — Technology Stack  
7. `@AI-STEP-07` — Design System  
8. `@AI-STEP-08` — AI Operating Model  
9. `@AI-STEP-09` — Execution Backlog  
10. `@AI-STEP-10` — Repository Blueprint  

**Do not skip steps.**  
Skipping steps increases architectural risk.

---

## How to Use

### Option A — Tag the Template
If your AI tool supports file tagging:

```
@AI-STEP-01
```

Then optionally add context:

```
@AI-STEP-01

I want to build a platform for...
```

The AI will begin discovery automatically.

---

### Option B — Copy/Paste
Simply paste the template into your AI session and start.

---

## Interaction Pattern

Each step is designed to be interactive.

The AI will:

- Ask structured questions
- Prefer multiple-choice where possible
- Surface assumptions
- Challenge unclear thinking
- Identify risks
- Produce a document

You should:

- Answer concisely
- Correct misunderstandings early
- Push for simplicity
- Avoid premature tech discussions

When satisfied, tag the next step.

---

## Artifacts Produced

By the end of the workflow you will have:

- Business Context document  
- PRD  
- Risk Review  
- Decision Log  
- Architecture  
- Technology Stack  
- Design Manual  
- AI Governance Framework  
- Structured Backlog  
- Repository Blueprint  

This is an unusually strong foundation for a greenfield system.

Most teams never reach this level of clarity.

---

## Important Rules

### Do Not Start With Code
The cost of redesigning architecture mid-build is enormous.

### Do Not Let AI Invent Structure
Structure should emerge from deliberate decisions.

### Prefer Simplicity
Every abstraction is future maintenance.

### Challenge Complexity
When the AI proposes something complex, ask:

> “What is the simplest solution that would still be correct?”

---

## When To Stop Designing

You are ready to begin implementation when:

- Architecture feels calm  
- Tradeoffs are explicit  
- Risks are understood  
- The backlog is executable  

At that point, generate the repository and begin coding.

---

## Who This Is For

This framework is especially valuable for:

- AI-first development teams  
- Solo builders  
- Technical founders  
- Product engineers  
- Greenfield systems  
- Internal tooling  

It is less necessary for trivial prototypes.

---

## Expected Outcome

If followed carefully, this workflow dramatically increases the probability that you will build:

- A stable system  
- An evolvable architecture  
- A coherent codebase  
- A maintainable product  

Instead of an improvised one.

---

## Final Principle

When uncertain, ask:

> Does this decision make the system calmer — or more complicated?

Choose calm.

Calm systems endure.
