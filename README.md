# LG-EYEAR — Proactive Home Orchestration & 3D Simulation

**EYEAR: Eyes and Ears for Proactive Smart Home Orchestration through Spatial Awareness and Multi-Agent Collaboration**

Main integration repository for the EYEAR academic prototype (Hanyang University, Fall 2026; CSE406 / ITE351).

> **Status:** Architecture and requirements defined; implementation status and setup instructions will be updated as components become executable. This repository does not imply official LG ThinQ ON integration or physical appliance control.

## Scope

1. Ingest validated, timestamped **Semantic Events** from emulated EYEAR Nodes or authored scenarios.
2. Maintain a multi-room **Home World Model** with occupancy, identity uncertainty, activity hypotheses, appliance states, and event history.
3. Request **role-based agents** to produce structured proposals or restrictions (initially **Cleaning** and **Activity/Quiet**).
4. Use a **Home Orchestrator** to select/replan tasks; support an optional pretrained LLM supervisor for contextual interpretation and explanations.
5. Enforce **deterministic policies**, device capabilities, user overrides, and safety restrictions before action execution.
6. Send **Action Plans** to the 3D smart-home virtual-appliance adapter and receive **Action Results**.
7. Replay multiple recorded sensor sources on a common scenario clock, with inference executed in the [AI repository](https://github.com/HY-LG-EYEAR/LG-EYEAR-ai).

## Core Pipeline

```text
Live/Recorded Node Adapter ─┐
                            ├→ Semantic Event API → World Model → Domain Agents
3D Scenario Input ──────────┘                                    │
                                                        Home Orchestrator
                                                        (optional LLM)
                                                               │
                                                      Policy Validator
                                                               │
                                                      Action Plan / API
                                                               │
                                              3D Virtual Appliances → Feedback
```

## Initial Demonstration Scenarios

**Adaptive robot cleaning** — Choose feasible rooms based on occupancy, activity restrictions and remaining cleaning work; replan when an occupant enters an intended room.

**Activity-aware quiet coordination** — Combine room occupancy, speech-activity signals and optionally simulated meeting status to infer a *possible* noise-sensitive situation; coordinate virtual robot-vacuum and laundry decisions. Do not treat speech alone as meeting proof.

The 3D client is an interactive execution/visualization environment, **not** a substitute for running the central decision pipeline.

## Proposed Structure

```text
backend/
  api/                  # REST/WebSocket endpoints
  contracts/            # SemanticEvent, WorldState, AgentProposal, ActionPlan/Result
  event_ingestion/      # timestamp ordering, deduplication, validation
  world_model/          # room / people / device states
  agents/               # cleaning, quiet/activity; other roles when justified
  orchestration/        # conflict resolution / optional LLM interface
  policy/               # hard restrictions and capabilities
  adapters/             # virtual appliance actions / feedback
replay/
  clock/                # shared replay clock
  scenarios/            # manifests and non-sensitive scenario descriptions
simulation/
  headless/             # deterministic scenarios / optional RL environments
  evaluation/           # fixed-rule vs replanning comparisons
digital-twin/           # Unity or Godot project (engine to be selected)
tests/
  unit/
  integration/
  scenarios/
```

## Shared Contracts (to be versioned)

- `SemanticEvent`: `schema_version`, `event_id`, `node_id`, `timestamp`, `room_id`, `observation_type`, `value`, `quality`.
- `WorldState`: timestamped room, person/track, activity-hypothesis, and appliance state snapshot.
- `AgentProposal`: proposed actions, applicability, constraints, expected effects, reason codes.
- `ActionPlan`: selected virtual commands, preconditions, priority, traceable plan ID.
- `ActionResult`: accepted/rejected/completed/failed, execution timestamp, failure reason.

**Contract tests** must ensure sensor replay and authored scenarios enter the same pipeline.

## Testing and Evaluation

- Room occupancy and unknown-state handling
- Proposal conflict resolution and explicit override precedence
- Replanning after significant context change
- Rejection of malformed events or unsupported commands
- Perception-to-decision and decision-to-visualization latency
- Repeatability of synchronized replay

## Planned Development Stack

Python / FastAPI / Pydantic for central services; MQTT or WebSocket/REST for messaging; Unity or Godot for 3D; optional OR-Tools for planning. Exact versions, hardware, costs, and design rationale will be documented in the [CSE406 Specification](https://github.com/HY-LG-EYEAR/LG-EYEAR-docs). Do not treat these choices as already implemented.

## Related Repositories

- [LG-EYEAR-ai](https://github.com/HY-LG-EYEAR/LG-EYEAR-ai)
- [LG-EYEAR-docs](https://github.com/HY-LG-EYEAR/LG-EYEAR-docs)
- [LG-EYEAR-blog](https://github.com/HY-LG-EYEAR/LG-EYEAR-blog)
