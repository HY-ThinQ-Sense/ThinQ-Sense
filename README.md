# ThinQ Sense — System Prototype

The integrated research prototype for **ThinQ Sense**, developed for Hanyang University CSE406 and ITE351 (Fall 2026).

## Scope

- Accept normalized sensor events from live sensing or scenario simulation.
- Maintain person, room, device and environment state in a household world model.
- Generate context-based predictions, constraints and appliance action intents.
- Visualize decisions and state transitions in a 2D digital twin.
- No real appliance actuation is assumed in the initial milestone.

## Architecture

```text
Live Sensor Adapter ─┐
                     ├─ Event API → World Model → Planner → Virtual Appliance Adapter
Scenario Simulator ──┘                                   │
                                                     Digital Twin UI
```

## Suggested Structure

```text
backend/          # event ingestion, world model, policy and planner
frontend/         # dashboard and 2D digital twin
contracts/        # shared JSON Schema / event and action schemas
simulator/        # deterministic scenario inputs
scripts/          # local setup and test helpers
tests/            # integration and scenario tests
```

## Initial Demonstrations

1. A sleeping occupant causes the robot vacuum to avoid that room.
2. The cleaning order changes as occupants move.
3. Bedtime context produces proposed multi-appliance actions.

## Development Status

Planning / requirements analysis. Setup, commands, and links will be updated after the implementation stack is selected.

## Related Repositories

- [Perception and AI](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-ai)
- [CSE406 documents](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-docs)
- [ITE351 blog](https://github.com/HY-ThinQ-Sense/ThinQ-Sense-blog)
