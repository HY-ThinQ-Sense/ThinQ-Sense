# ThinQ Sense — Multi-Agent Home Orchestration & 3D Digital Twin

**Main System Repository**

> A Spatially Aware Multi-Agent System for Predictive and Proactive Smart Home Orchestration

## Overview

This repository contains the main software system for ThinQ Sense, including the household world model, multi-agent planning engine, policy validation, simulation environment, and interactive 3D digital twin.

The system receives structured semantic events from perception modules or simulated scenarios, maintains the current household state, predicts future conditions, and generates coordinated appliance action plans.

The prototype uses simulated appliance execution rather than controlling physical LG appliances.

## Core Architecture

```text
Live Sensor Adapter ----+
                        |
Scenario Simulator -----+--> Event Ingestion
                                |
                                v
                         Home World Model
                                |
                                v
                         Prediction Service
                                |
                                v
                        Multi-Agent System
                       /        |        \
                 Cleaning    Climate    Quiet
                   Agent      Agent     Agent
                       \        |        /
                                v
                         Home Orchestrator
                                |
                      Optimization & Policy
                                |
                                v
                          Action Planner
                                |
                         Virtual Actuators
                                |
                                v
                       3D Smart Home Digital Twin
                                |
                         Execution Feedback
                                |
                                +----> World Model
```

## Major Components

### 1. Event Ingestion

Receives and validates structured events from real perception pipelines and virtual scenario inputs.

Responsibilities:

- Schema validation
- Timestamp management
- Duplicate detection
- Event normalization
- Source identification

### 2. Home World Model

Maintains household state, including:

- Occupant identity and current room
- Human posture and activity
- Room occupancy and environmental conditions
- Appliance status and capabilities
- User preferences and automation policies
- Context history and state transitions

### 3. Prediction Service

Estimates future household conditions such as:

- Next room transitions
- Expected room occupancy
- Activity transitions
- Potential task interruption windows

Prediction results are represented probabilistically and are not treated as confirmed observations.

### 4. Specialized Agents

**Cleaning Agent**

Plans adaptive robot vacuum operations according to occupancy, cleaning requirements, estimated travel costs, and user disturbance constraints.

**Climate Agent**

Proposes environmental adjustments based on room occupancy, activity, comfort preferences, and energy considerations.

**Quiet Agent**

Generates disturbance-related restrictions during sleep, meetings, and other noise-sensitive activities.

**Laundry / Scheduling Agent**

Schedules eligible appliance tasks while considering deadlines, device capabilities, and household constraints.

### 5. Global Home Orchestrator

Coordinates proposals from specialized agents.

Responsibilities:

- Goal prioritization
- Conflict detection
- Hard and soft constraint management
- Global plan optimization
- Dynamic replanning
- Decision explanation
- Action intent generation

### 6. Decision Learning

The project will compare several decision-making approaches:

- Fixed schedules
- Reactive rules
- Predictive constraint optimization
- Optional reinforcement learning policies

Constraint optimization will be developed as the main planning baseline. Reinforcement learning will be evaluated as an additional learning-based method when feasible.

### 7. 3D Smart Home Digital Twin

An interactive 3D simulation environment visualizes:

- Household rooms and connected spaces
- Virtual occupants and activities
- Appliance states
- Robot vacuum movement and route replanning
- Agent proposals and orchestration decisions
- Execution feedback

The simulation supports both live sensor events and scripted virtual scenarios through a common event interface.

## Proposed Repository Structure

```text
backend/
  api/
  contracts/
  event_bus/
  world_model/
  prediction/
  agents/
  optimizer/
  policy/
  adapters/

simulation/
  scenario_generator/
  home_environment/
  gym_env/
  baselines/
  rl_training/

digital-twin/
  scenes/
  scripts/
  assets/
  avatars/
  appliances/

tests/
  unit/
  integration/
  scenarios/

configs/
scripts/
```

## Data Contracts

The system uses three main interfaces:

- **SemanticEvent:** Perception output describing observed occupants and spaces.
- **WorldState / Prediction:** Current and predicted household conditions.
- **ActionPlan / ActionResult:** Structured appliance decisions and simulated execution feedback.

These contracts must be shared with the AI repository and the 3D client.

## Core Demonstration Scenarios

1. **Adaptive Cleaning:** Replan cleaning routes when room occupancy changes.
2. **Predictive Sleep:** Prepare home environments using predicted activity transitions.
3. **Quiet Home:** Coordinate multiple appliance operations during noise-sensitive activities.
4. **Privacy Mode:** Continue limited presence-based automation when camera sensing is disabled.

## Evaluation

The system will evaluate:

- Task completion rate
- Disturbance events
- Constraint violations
- Planning and replanning latency
- Estimated energy and travel costs
- Performance relative to fixed schedules and rule-based baselines

## Development Status

**Planning and early implementation.**

The proposed architecture and features represent development targets, not completed functionality.

## Related Repositories

- [AI & Perception](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-ai)
- [Software Engineering Documentation](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-docs)
- [AI Technical Blog](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-blog)
