# Part 1: Spoken Language Models — mapping the landscape

**Date:** Oct 5 2025 — **Estimated reading time:** ~15 min

## Table of contents

- [Part 1: Spoken Language Models — mapping the landscape](#part1-spoken-language-models--mapping-the-landscape)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Why spoken language models?](#why-spoken-language-models)
  - [A taxonomy of spoken language models](#a-taxonomy-of-spoken-language-models)
    - [Pure speech language models](#pure-speech-language-models)
    - [Speech+text language models](#speechtext-language-models)
    - [Speech‑aware text language models](#speechaware-text-language-models)
  - [What makes a universal SLM?](#what-makes-a-universal-slm)
  - [Closing thoughts](#closing-thoughts)
  - [Looking ahead](#looking-ahead)

---

## Introduction

The past decade of natural language processing (NLP) has shifted from building narrowly focused models for specific tasks to training massive language models (LLMs) capable of solving a wide range of textual problems with minimal adaptation.  Speech processing is following a similar trajectory: early systems combined a **speech recognizer**, **text LLM** and **text‑to‑speech synthesizer** in a cascaded pipeline.  While effective for many tasks, these pipelines lose **non‑linguistic information**—such as speaker identity, emotion and prosody—and accumulate errors as each component feeds into the next.

Spoken language models (SLMs) aim to unify these stages.  An SLM is a neural model that can process and generate spoken signals directly, optionally interacting with written text.  This article introduces the core classifications of SLMs defined in a comprehensive survey and sets the stage for later discussions on training, architecture and evaluation.

## Why spoken language models?

At first glance, connecting a speech recognizer to a text LLM and then to a speech synthesizer appears sufficient.  Indeed, for tasks where only the **lexical content** matters—such as dictation or retrieving factual information—this pipeline remains a strong baseline.  However, many applications require more than words.  Consider tasks like **emotion recognition**, **speaker identification**, **prosody‑aware dialogue** or **expressive voice cloning**.  In these cases, summarizing the audio as text loses vital cues.  End‑to‑end SLMs retain these nuances and avoid error compounding across modules.

Additionally, SLMs can naturally support **spoken instructions**, enabling voice agents that do not rely on a screen or keyboard.  As we move toward more natural human–AI interaction, the ability to understand and generate speech becomes essential.

## A taxonomy of spoken language models

The survey categorizes SLMs into three main types.  Each type is defined by the probabilistic distribution it models and the training data it requires.

### Pure speech language models

**Definition.** These models learn the distribution **p(speech)**—they generate or continue speech audio without reference to text.  Training typically involves a self‑supervised objective on untranscribed audio (e.g. predicting the next audio token or reconstructing masked segments).

**Examples.** Early examples include **GSLM** and **AudioLM**, which tokenise audio using a self‑supervised codec and then train a language model over the resulting tokens.  Such models can generate realistic speech continuations or learn useful speech representations.

**Use cases.** Pure speech LMs are valuable for tasks like unconditional audio synthesis, prosody learning and self‑supervised pre‑training of speech encoders.  They do not handle text inputs or outputs.

### Speech+text language models

**Definition.** These models learn the **joint distribution p(text, speech)**.  They are trained on paired audio–text data so they can generate both spoken and written outputs given either modality.  Think of them as multimodal language models that treat speech and text symmetrically.

**Examples.** Models like **SpiRit‑LM** and **Moshi** fall into this category.  They can perform speech‑to‑speech translation, speech‑to‑text transcription and text‑to‑speech synthesis within a unified framework.

**Use cases.** Multilingual translation, spoken dialogue systems and any application where the model needs to produce both text and audio responses.  Because they handle both modalities natively, they avoid the mismatch of training separate ASR and TTS models.

### Speech‑aware text language models

**Definition.** These models begin with a **pretrained text LLM** and augment it with a speech encoder.  They model **p(text | speech, text)**—given a spoken input and a textual instruction, generate a textual response.  The key idea is to reuse the LLM’s ability to follow complex instructions while adding the capacity to comprehend audio.

**Examples.** Models such as **SALMONN** and **Qwen‑Audio‑Chat** use a speech encoder (e.g. Whisper) to produce discrete speech tokens, which are then fed into a decoder‑only LLM alongside the instruction text.

**Use cases.** Spoken question answering, voice assistants and summarization.  These systems produce text; if a spoken response is needed, a separate TTS component can follow.

## What makes a universal SLM?

The survey introduces a **functional definition** of a universal speech processing system:

1. **Bidirectional speech.** The model must accept spoken input and produce spoken output, with optional text input/output.
2. **Task universality.** It should, in principle, handle any spoken task, from recognition and translation to reasoning about audio.
3. **Natural‑language prompts.** Instructions should be given in natural language (spoken or written), not restricted to task tokens or soft prompts.

Most existing models do **not** satisfy all these criteria yet.  Pure speech LMs rarely produce spoken output conditioned on natural‑language prompts; speech+text LMs often require paired text instructions; and speech‑aware text LMs output text only.  Nevertheless, these categories are stepping stones toward universal SLMs.

## Closing thoughts

By categorizing SLMs into **pure speech**, **speech+text** and **speech‑aware text** models, the survey clarifies the design space and aligns it with the evolution of text LMs.  This unified terminology will help researchers compare new models fairly and identify which components need improvement.  Pipelines remain a strong baseline, especially when prosody is unimportant and resources are limited.  Yet the potential of end‑to‑end SLMs to retain prosody, reduce latency and simplify training is compelling.

A word of caution: while categories aid navigation, the field is evolving rapidly.  Some models blur boundaries—for example, they may generate text and speech in different stages.  Keep the **functional goals** in mind rather than clinging to labels.  In later parts, we will explore how these models are built, trained and evaluated.

## Looking ahead

This first installment has laid out the basic landscape and definitions.  **Part 2** will dive into the *architecture* of SLMs: how speech encoders, alignment modules and sequence models fit together.  **Part 3** will examine *training strategies*—from pre‑training on unlabeled audio to instruction tuning.  By following the survey’s structure, we’ll build a cohesive understanding of this exciting field.
