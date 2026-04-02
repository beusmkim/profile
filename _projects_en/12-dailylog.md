---
layout: project
title: "DailyLog — On-Device Voice AI Pipeline & Adaptive Recommendation System"
summary: "End-to-end voice journaling system: int8-quantized on-device ASR, slot-driven LLM agent, and Thompson Sampling-based personalized activity recommendation"
period: "2025-2026"
role: "AI · Backend · Android"
stack: "SenseVoice Small, sherpa-onnx, Claude Sonnet, FastAPI, Kafka, pgvector, PostgreSQL, Kotlin Compose"
image: /assets/img/projects/daily_log_main.png
category: hardware
priority: 2
order: 20
featured: true
---

## Award

**Excellence Award — SSAFY Special Project** (Samsung Software Academy For Youth, 2026)

---

## Overview

DailyLog is an AI-powered daily wellness journaling system built around a fully on-device voice pipeline.
The core design constraint: minimize perceived latency while running ASR, LLM inference, and TTS entirely without server round-trips where possible.

Key engineering focus areas:
- On-device int8-quantized ASR with simultaneous emotion classification
- Slot-based LLM agent for structured diary extraction via natural conversation
- Thompson Sampling-based multi-armed bandit for personalized activity recommendation

---

## Problem

Existing journaling tools required manual text input, creating friction that reduced daily completion rates.
A voice-first approach introduced three compounding technical constraints:

- ASR on mobile must be fast enough to feel real-time (target: sub-400ms)
- LLM-driven conversation must extract structured data reliably without rigid prompts
- Recommendation must balance exploration of unseen activities with exploitation of proven ones

Solving any one in isolation was straightforward. Solving all three within a single low-latency pipeline required constraint-aware design at each layer.

---

## Architecture

Three independent subsystems, each optimized for its own bottleneck:

```
[Voice Input]
     │
     ▼
[ASR: SenseVoice Small / sherpa-onnx]  ← int8 on-device
     │  Korean transcript + emotion tag (7-class)
     ▼
[LLM Agent: Claude Sonnet / FastAPI]   ← GMS Anthropic proxy
     │  Slot extraction (7 slots) → diary generation
     ▼
[TTS: Android Built-in]                ← on-device, no network
     │
     ▼
[Recommendation Engine]                ← Thompson Sampling + pgvector
```

---

## Subsystem 1 — On-Device ASR Pipeline

### Model Selection

SenseVoice Small was selected over Whisper-class models for two reasons:
- Joint ASR + Speech Emotion Recognition (SER) in a single forward pass
- Smaller footprint compatible with int8 quantization on Android ARM

### Quantization Strategy

The FP32 model was converted to int8 via sherpa-onnx's static quantization pipeline:
- Calibrated on Korean conversational speech samples
- Weight-only quantization applied to attention and FFN layers
- Activations kept at FP32 at numerically sensitive paths to prevent accuracy collapse

Result: model footprint reduced ~4x vs FP32, enabling stable on-device execution without OOM on mid-range Android devices.

### Emotion Tag Extraction

SenseVoice Small outputs 7-class emotion labels (HAPPY, SAD, ANGRY, DISGUSTED, FEARFUL, SURPRISED, NEUTRAL) simultaneously with transcription.
These emotion signals are passed directly into the LLM agent's slot-filling context, reducing the need for the model to infer emotional state purely from text.

### Korean Colloquial Correction

ASR models trained on read speech systematically misrecognize Korean colloquial speech:
- Contracted forms (어떡해 → 어떻게 해) and sentence-final particles
- Informal verb endings (했어, 했지, 했거든) that diverge from formal forms

A rule-based post-processing layer was applied to correct high-frequency colloquial patterns before passing transcripts to the LLM agent.
This reduced downstream slot-filling errors caused by ASR normalization artifacts.

### Latency Result

On-device ASR inference achieved ~300ms end-to-end on target Android hardware — within the perceptual threshold for natural turn-taking.

![ASR on-device inference]({{ '/assets/img/projects/daily_log_asr.png' | relative_url }})

---

## Subsystem 2 — Slot-Based LLM Agent

### Slot Schema

The agent extracts 7 structured slots from a multi-turn conversation:

| Slot | Content |
|------|---------|
| `event` | What happened today |
| `emotion` | How the user felt |
| `cause` | Why they felt that way |
| `highlight` | Best moment of the day |
| `challenge` | Difficulty or struggle |
| `tomorrow` | Goal or plan for tomorrow |
| `reflection` | Overall reflection |

### Conversation Management

Each turn, the agent:
1. Inspects the current slot-fill state
2. Identifies the highest-priority unfilled slot
3. Generates a contextually appropriate follow-up question in casual Korean (반말 persona)
4. Updates slot state on response

The system prompt was engineered to maintain consistent persona (friendly, casual, empathetic) while reliably extracting structured data — a tension that required careful prompt design to resolve.
Early versions produced either robotic slot-collection behavior or inconsistent extraction; the final design separates extraction logic from persona tone at the prompt level.

### Diary Generation

Once all 7 slots are filled, the agent synthesizes a first-person Korean diary entry:
- Draws from slot values to build narrative coherence
- Preserves the user's emotional tone from both text and ASR emotion tags
- Generates in natural Korean prose, not a structured summary

### Infrastructure

- Claude Sonnet accessed via GMS (Google Mobile Services) Anthropic proxy
- FastAPI server handles session state, slot tracking, and prompt assembly
- Conversation context maintained in Redis per session with TTL-based expiry

---

## Subsystem 3 — On-Device TTS

Android's built-in TTS engine was chosen over server-side synthesis for a single reason: latency.

Server TTS requires a full network round-trip — synthesis request, audio encoding, transfer, buffering.
On mid-range Android hardware under typical network conditions, this accumulated to 1.4–2.0s of perceived silence between the user's response and the agent's next question.

Switching to Android's on-device TTS engine eliminated network dependency entirely:
- Audio synthesis happens locally, in-process
- No encoding/transfer overhead
- Response latency reduced to under 50ms

The trade-off is voice quality. Server TTS produces more natural prosody.
The decision was made in favor of conversational rhythm over audio fidelity — a 50ms response feels like a conversation; a 2s pause breaks it.

![TTS latency comparison]({{ '/assets/img/projects/daily_log_tts.png' | relative_url }})

---

## Subsystem 4 — Personalized Recommendation Engine

### Design Goal

Recommend one activity per day that targets the user's lowest-scoring wellness axis.
The system must not repeatedly recommend the same activity (diversity), but also must not ignore activities that have consistently worked for a user (exploitation).

### 5-Stage Pipeline

**Stage 1 — Wellness State Analysis**
The LLM extracts 6-axis wellness scores from the completed diary:
- Stability / Achievement / Energy / Connection / Joy / Ease
The axis with the lowest score is selected as the targeting dimension for the day.

**Stage 2 — Candidate Recall**
Top-6 activities are recalled from the catalog filtered by:
- Same age group and gender cohort
- Alignment with the targeted wellness axis

**Stage 3 — Multi-Signal Scoring**
Each candidate receives a composite score from 6 independent signals:

| Signal | Description |
|--------|-------------|
| Axis fit | Alignment with the targeted wellness axis |
| Cohort score | Popularity within same age/gender segment |
| Interest score | Similarity to user's declared interests |
| Context score | Temporal and situational relevance |
| Similar-user score | pgvector cosine similarity against diary embeddings of similar users |
| MAB score | Thompson Sampling-derived exploration score |

**Stage 4 — Diversity Penalty & Final Selection**
A recency-based diversity penalty is applied to activities recommended in the past 7 days.
Final score = weighted composite − diversity penalty → Top-1 selected.

**Stage 5 — Feedback Learning**
User feedback (completed / skipped) is stored per activity per user.
Alpha/beta parameters of each activity's Beta distribution are updated accordingly, improving future MAB scores.

### Thompson Sampling vs Alternatives

| Algorithm | Weakness |
|-----------|----------|
| Epsilon-greedy | Exploration rate is static; does not adapt to observed reward variance |
| UCB | Assumes bounded reward distribution; overestimates confidence early |
| Thompson Sampling | Samples from posterior Beta(α, β); naturally balances exploration and exploitation as data accumulates |

Thompson Sampling was chosen because it adapts exploration intensity to actual uncertainty — giving new activities a fair chance while converging toward reliable recommendations over time.

![Thompson Sampling bandit scoring]({{ '/assets/img/projects/daily_log_bandit.png' | relative_url }})

### Recommendation Pool Expansion via Kafka

When a user reports a positive emotional outcome (HAPPY) during checkin, the activity associated with that moment is published as an event to a Kafka topic.
A consumer monitors this stream: if an activity accumulates 3+ occurrences with 2+ positive feedback events across users, it graduates to the permanent recommendation catalog.

This creates a feedback loop where the catalog grows organically from real user behavior — without manual curation.

### pgvector Similarity Search

Each diary entry is embedded via a text embedding model and stored in PostgreSQL with the pgvector extension.
At recommendation time, the user's latest diary embedding is used to search for similar past entries across all users via cosine similarity.
Activities associated with those similar contexts are scored positively in the similar-user signal.

---

## Result

| Metric | Before | After |
|--------|--------|-------|
| Diary completion time | ~20 min | ~5 min |
| Reduction | — | ~70% |
| ASR inference latency | N/A (server-side) | ~300ms (on-device) |
| TTS response latency | 1.4–2.0s (server TTS) | <50ms (on-device) |
| Slot extraction | Manual input | 7 slots auto-extracted |
| Recommendation diversity | Static list | MAB-adaptive |

---

## Key Insight

The 300ms ASR target was achievable only because quantization and model selection were treated as co-design decisions, not post-hoc compression.
The LLM agent's reliability came from separating persona from extraction at the prompt level — not from a more capable model.
The recommendation system's value emerged from the 5-stage pipeline architecture, not from any single algorithm — Thompson Sampling alone without the similarity and cohort signals would have produced surface-level personalization.

Each subsystem's constraint defined the solution. Measurement before optimization was the consistent principle.

---

## Screenshots

![DailyLog Team]({{ '/assets/img/projects/daily_log_team.JPG' | relative_url }})
![DailyLog Main]({{ '/assets/img/projects/daily_log_main.png' | relative_url }})
![DailyLog Checkin]({{ '/assets/img/projects/daily_log_checkin.png' | relative_url }})
![DailyLog Diary]({{ '/assets/img/projects/daily_log_diary.png' | relative_url }})
![DailyLog Calendar]({{ '/assets/img/projects/daily_log_callendar.png' | relative_url }})
![DailyLog Emotion Graph]({{ '/assets/img/projects/daily_log_감정그래프.png' | relative_url }})
