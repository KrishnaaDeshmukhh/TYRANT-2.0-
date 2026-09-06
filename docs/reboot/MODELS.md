# TYRANT Reboot — Models

Status: EXPLORING

## Current Direction

TYRANT should use model/provider adapters rather than hardcoding a single AI vendor. Model choice should be capability- and economics-driven.

## Known Requirements

Different tasks may need different model characteristics:
- research and synthesis
- script/story generation
- hook/title generation
- content scoring
- visual planning
- image generation
- illustrated/stickman scene generation
- video generation where justified
- speech/TTS
- transcription
- quality control

## Economic Principle

Prefer free/open-source models, free API tiers/credits, and available cloud/GPU credits during initial operation. Paid models/services can be introduced when revenue justifies the additional cost or when quality/throughput requires them.

## Current Decisions

No single final model/provider stack has been locked during the current reboot content-type evaluation. Provider decisions should follow confirmed pipeline requirements rather than precede them.

## Open

Exact model assignments, fallback chains, local-vs-API boundaries, GPU requirements, and quality benchmarks remain open.
