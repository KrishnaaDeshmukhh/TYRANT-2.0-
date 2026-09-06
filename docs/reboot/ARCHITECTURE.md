# TYRANT Architecture

Status: EXPLORING

## Core Architectural Direction

TYRANT should be a **job-driven autonomous content factory**, not a collection of rigid, hardcoded pipelines. The confirmed content types should compose reusable capabilities.

Conceptually:

```text
Content Objective / Producer
          ↓
     Content Type Plan
          ↓
      Job Creation
          ↓
        Queues
          ↓
 Resource-Aware Scheduler
          ↓
 Research → Script → Visual Plan → Assets → Voice → Edit
          ↓
       Quality Control
          ↓
      Distribution
          ↓
 Analytics → Revenue → Learning
          ↺
```

## Reusable Capabilities

Candidate workers/capabilities include:
- Producer / Content Planner
- Content Researcher
- Scriptwriter
- Hook/Title Generator
- Story / Narrative Planner
- Asset Planner / Visual Director
- Image Generator
- Illustration / Stickman Scene Generator
- B-roll Finder/Generator
- Gameplay Background Selector
- Product / Brand Asset Collector
- Voice Generator
- Video Generator
- Editor / Compositor
- Captioner
- Audio/Mixing Worker
- Quality-Control Worker
- Distributor
- Analytics Collector
- Revenue/Attribution Worker

The exact worker set remains open. A capability should be added when multiple content types can benefit from it.

## Visual Director

A major shared abstraction is the **Visual Director**. It should translate narration/script beats into visual requirements and select an appropriate treatment instead of forcing every content type into one visual style.

Candidate treatments already identified:
- reusable Minecraft gameplay as an attention/background layer
- screenshots and product images for recommendation content
- generated images/graphics
- illustrated/stickman animated scenes
- motion graphics/text overlays
- AI video only where its quality/cost justifies it
- real presenter footage for the conditional AI-presenter format

The Visual Director should optimize for attention, clarity, cost, and available assets.

## Content-Type Composition

Examples:

```text
Storytelling
→ story plan
→ voice
→ Minecraft background
→ attention visuals/captions
→ edit

Animated Explainer
→ research
→ explanation script
→ illustrated scene plan
→ stickman scenes
→ voice
→ edit

List / Recommendation
→ research
→ ranked items
→ product/brand assets
→ screenshots/images/demos where useful
→ comparison visuals
→ voice
→ edit
→ affiliate packaging
```

The examples are format patterns, not separate software systems.

## Workers, Not Fixed Pipelines

A worker is a reusable capability. For example, an Editor should process editing jobs from many content types, while a Visual Director chooses which visual treatment a particular job requires.

Workers should advertise capabilities and resource requirements. Multiple workers can execute concurrently subject to CPU, GPU, RAM, storage, API quota, cost, and priority.

## Queue-Based Execution

Work should flow through queues rather than direct worker-to-worker calls. A completed job emits an event/state transition that makes dependent work eligible.

```text
Research complete
      ↓
Script eligible
      ↓
Visual plan eligible
      ↓
Assets eligible
      ↓
Edit eligible
      ↓
QC eligible
      ↓
Distribution eligible
```

## Resource-Aware Scheduling

The scheduler should eventually consider GPU VRAM/utilization, CPU, RAM, storage/I/O, model requirements, execution time, queue depth, priority, production cost, free/cloud/API credits, and retry state.

## Status

The job/worker/resource model and reusable capability approach are strong current directions. Exact queue technology, event implementation, worker runtime, scheduler implementation, infrastructure, and final capability contracts remain undecided.
