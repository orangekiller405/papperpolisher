---
name: "paper_polisher"
description: "Hierarchical academic writing system for CV papers. Translates and polishes into CVPR/TPAMI/NeurIPS style. Invoke for translation, rewriting, or section-specific polishing."
---

# Paper Polisher (Academic Writing Policy System)

This is a hierarchical skill designed to rewrite Chinese or non-native English manuscripts into top-tier academic English (CVPR, ICCV, TPAMI, etc.) by applying specific writing policies in stages.

## Core Capabilities

### 1. Full-Text Processing (Orchestrator Mode)
- **Automatic Splitting**: Ingests a full manuscript and splits it into logical sections (Abstract, Intro, Method, Experiments, Conclusion).
- **Sequential Application**: Processes each section using its specific policy (from `prompts/`) and the target style (from `styles/`).
- **Context Preservation**: Maintains terminological consistency across the entire document.

### 2. Style Miner (On-the-fly Adaptation)
- **Dynamic Corpus Building**: If a requested venue (e.g., "Elsevier", "EAAI") is missing from `styles/`, the system will:
    1.  Search for recent top-cited papers using `keywords` + `target_venue`.
    2.  Extract rhetorical statistics (sentence length distribution, claim strength, transition patterns).
    3.  Generate and save a new `<venue>.md` in `styles/`.
- **Domain Alignment**: Adapts the tone specifically to the research field (e.g., Diffusion Models, Industrial Inspection).

## Routing Logic

When invoked, follow this hierarchical workflow:

### Stage 1: Context & Mode Detection
- **Full-Text vs. Snippet**: If a file is provided, enter "Full-Text Mode".
- **Venue & Keywords**: Check if the requested venue exists. If not, trigger the **Style Miner**.
- **Section Detection**: Identify sections using header patterns.

### Stage 2: Policy Injection (Per Section)
1.  **Load Global Policy**: Always inject `prompts/global.md`, `banned_patterns.yaml`, and `rewrite_rules.yaml`.
2.  **Load Style Prior**: Load the venue-specific rhetorical distribution (existing or newly mined).
3.  **Apply Section Policy**: Switch policies as the parser moves from Intro to Method, etc.

### Stage 3: Execution & Reconstruction
- **Preservation**: Lock equations and citations.
- **Bilingual Output**: Generate a paragraph-level comparison for the entire file.
- **Full Reconstruct**: Output a clean, polished version of the complete manuscript.

## Invoke Policy

Invoke this skill when the user asks to:
- "Polish my paper"
- "Translate this abstract/intro/method"
- "Rewrite for [CVPR/TPAMI/NeurIPS]"
- "Compress this section"

## Output Format

1.  **Polished Text**: The primary rewritten output.
2.  **Revision Report**: A brief summary of key changes (e.g., "Compressed Intro by 20%", "Removed AI-style abstractions").
3.  **Bilingual Alignment (Optional)**: Paragraph-level comparison if requested.

## Directory Structure
- `prompts/`: Section-specific writing strategies.
- `styles/`: Venue-specific rhetorical priors.
- `banned_patterns.yaml`: Words and phrases to avoid.
- `rewrite_rules.yaml`: Core rewriting and compression logic.
