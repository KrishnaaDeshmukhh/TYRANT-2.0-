# TYRANT Architecture

Status: EXPLORING

## Core Architectural Direction

TYRANT should be designed as a **job-driven autonomous content factory**, not as a collection of rigid, hardcoded pipelines.

The system should decompose content production into reusable jobs and route those jobs to workers based on capability, availability, priority, dependencies, and resource constraints.

Conceptually:

```text
Producer / Content Planner
          ↓
      Job Creation
          ↓
        Queues
          ↓
 Resource-Aware Scheduler
          ↓
 ┌────────┬────────┬────────┐
 Research Creation  Media   Operations
 Workers   Workers  Workers  Workers
 └────────┴────────┴────────┘
          ↓
      Quality Control
          ↓
      Distribution
          ↓
       Analytics
          ↓
       Revenue / Learning
          ↓
        Producer
```

## Workers, Not Fixed Pipelines

Example workers include:
- Producer
- Content Researcher
- Scriptwriter
- Hook/Title Generator
- Asset Planner
- Image Generator
- B-roll Finder/Generator
- Voice Generator
- Video Generator
- Editor
- Captioner
- Audio/Mixing Worker
- Quality-Control Worker
- Distributor
- Analytics Collector
- Revenue/Attribution Worker

This list is illustrative, not final. Workers should be added when a reusable capability is needed.

A single worker type should be able to process many jobs. For example, an Editor is not one process permanently assigned to one video. Multiple editor workers can consume editing jobs concurrently, subject to CPU, GPU, RAM, storage, and encoding capacity.

## Dynamic Parallelism

TYRANT should distinguish between:

- **Jobs existing in the system**
- **Jobs waiting in queues**
- **Jobs actively executing**
- **Actual hardware concurrency**

For example, TYRANT may have 100 scripts queued, 20 script jobs actively running, and 2 GPU-heavy video-generation jobs running at the same time.

Concurrency should therefore be **resource-aware rather than hardcoded**.

Workers should advertise or expose capabilities and resource requirements. The scheduler can then decide which jobs can run and where.

Example worker metadata:

```text
Worker: VideoGenerator-01
Capabilities: text_to_video, image_to_video
GPU: A100 80GB
Concurrency: resource-dependent
Status: available
```

## Compute Abstraction

TYRANT should not be architecturally tied to a specific GPU model.

An A100 is an example of a high-capacity worker host, not an architectural dependency. The same scheduler should be able to use consumer GPUs, cloud GPUs, CPU workers, and API-based model providers where appropriate.

The system should adapt execution to available resources rather than assuming unlimited compute.

## Queue-Based Execution

Work should flow through queues rather than direct worker-to-worker calls. A completed job emits an event/state transition that makes dependent work eligible.

Example:

```text
Research complete
      ↓
Script job becomes eligible
      ↓
Script complete
      ↓
Asset jobs become eligible
      ↓
Assets complete
      ↓
Edit job becomes eligible
      ↓
QC complete
      ↓
Distribution job becomes eligible
```

This preserves the benefits of dependency-driven production without turning every content type into a separate hardcoded pipeline.

## Producer Role

The Producer is conceptually different from a worker that performs one media operation. It creates and prioritizes production work.

A Producer may turn a content objective into many candidate jobs, for example:

```text
Goal: produce 100 social videos

→ research candidates
→ select opportunities
→ create 100 content jobs
→ decompose each into required work
→ prioritize work
→ send work into queues
```

The Producer should optimize for TYRANT's business objective rather than artistic perfection for its own sake.

## Resource-Aware Scheduling

The scheduler should eventually consider:
- GPU VRAM
- GPU utilization
- CPU availability
- system RAM
- storage and I/O
- model requirements
- expected execution time
- queue depth
- job priority
- production cost
- available free/cloud/API credits
- retry/failure state

This enables TYRANT to increase throughput when more compute becomes available without redesigning the content system.

## Status

This architecture is **EXPLORING**. The job/worker/resource model is a strong current direction, but exact queue technology, event implementation, worker runtime, scheduler implementation, and infrastructure choices remain undecided.
