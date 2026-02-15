 
# Skill: Interaction meta-preferences

This document defines a small, persistent set of interaction preferences that reduce interruption fatigue while keeping rigor.

## Source Of Truth
- If `.agentic_profile.md` exists, treat `## Interaction Preferences` as authoritative defaults.
- If it does not exist (or fields are missing), use the defaults in this file.
- Do not copy `.agentic_profile.md` into project artifacts unless the user explicitly requests it.

## Defaults (If No Profile)
- Question mode: Natural
- Question batch size: 2 (cap is always 3)
- Interruption tolerance: Balanced
- Probing depth: Standard
- Defaults vs questions: Mixed

## Preference Fields (What They Change)

### Question Mode (Natural / Choice / Binary / Creative)
- Sets the default mode for questions in chat.
- The agent may temporarily switch modes if the chosen mode would block progress (e.g., use Binary to resolve a contradiction).

### Question Batch Size (1 / 2 / 3)
- Hard cap is always 3.
- If the user prefers fewer interruptions, prefer asking fewer questions even when the batch size is 3.

### Interruption Tolerance (Minimal / Balanced / Interactive)

Minimal:
- Ask only *blocking* questions.
- Prefer to proceed with explicit assumptions and a short "correct me if wrong" check.
- Prefer 1 question per turn.

Balanced:
- Ask blocking questions.
- Ask high-impact questions when they materially change scope, cost, or correctness.

Interactive:
- Ask blocking questions.
- Also ask important questions earlier (before drafting artifacts) to reduce rework.

### Probing Depth (Light / Standard / Deep)

Light:
- Do the minimum to safely proceed; focus on the next deliverable.
- Prefer defaults/assumptions for low-impact details.

Standard:
- Progressive narrowing (Explore -> Define -> Converge).
- Ask enough to lock direction + avoid obvious rework.

Deep:
- Actively hunt edge cases, failure modes, and constraints.
- Prefer clarifying questions over assumptions for high-impact areas.

## Ask Vs Assume (Decision Policy)
When information is missing, classify it:

1) Blocking (cannot proceed safely/correctly)
- Always ask.
- If the user cannot answer, park it as `[Blocking]` in `artifacts/<project_slug>/00_open_questions.md` and stop.

2) High-impact (changes scope, correctness, security, or cost)
- Ask if Interruption tolerance is Balanced/Interactive *or* Probing depth is Deep *or* Defaults vs questions is Prefer questions.
- Otherwise: pick a reasonable default, state it explicitly, and proceed.

3) Low-impact (cosmetic, reversible, non-critical)
- Prefer defaults/assumptions unless the user asked to be questioned.

Assumptions should be:
- Visible (1-5 bullets max),
- Testable (what would change if wrong),
- Easy to correct.

## Adaptive Probing Depth (How It Adjusts)
Even with fixed preferences, adjust probing depth when signals demand it:

Increase depth (ask more / confirm more) when:
- Security/privacy/authn/authz is involved.
- Production data, money, legal/compliance, or irreversible operations are involved.
- You detect contradictions across artifacts or user answers.
- A wrong assumption would be expensive to unwind.

Decrease depth (assume more / ask less) when:
- Work is reversible and low-risk.
- The user is giving short answers and wants forward motion.
- The user explicitly requests batching/minimal interruptions.

## User Overrides (Per Turn)
The user can override behavior for the next turn:
- `@mode natural|choice|binary|creative`
- `@batch 1|2|3`
- `@interrupt minimal|balanced|interactive`
- `@depth light|standard|deep`

The agent should follow overrides for that turn unless doing so would block progress or create an unsafe outcome.

## Feedback-Driven Adaptation (No Extra Ceremony)
Adjust without asking extra meta-questions:

- If the user repeatedly corrects assumptions, shift toward asking more high-impact questions.
- If the user repeatedly gives short answers or signals urgency, shift toward fewer questions + explicit assumptions.
- If Choice mode repeatedly yields "Write your own answer", switch back to Natural for the next batch.
