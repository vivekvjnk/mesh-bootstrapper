---
name: mesh-bootstrapper
description: Bootstraps, configures, and verifies an ABB Agent MESH (Modular Engineering & Skill Hypervisor) runtime instance on any target workspace. Pre-flights environment requirements (mesh CLI, Pi/Copilot live connectivity), deploys multi-agent topologies (triad, research, machine_manager, custom cards) with gemini-3.7-flash defaults, and brings up the MESH hypervisor server.
metadata:
  version: "1.1.0"
  author: ABB-Agent-MESH-Team
---

# MESH Bootstrapper

## Overview

The `mesh-bootstrapper` Engineering Capability Package (ECP) provisions a fully-functional **ABB Agent MESH** runtime environment on any directory. It enforces strict pre-flight requirements (verifying `mesh` CLI and live connectivity of either `pi` or `copilot` harnesses with an actual message test), sets up the `.agents/` workspace hierarchy, deploys Agent Cards for selected topologies (`triad`, `research`, `machine_manager`, or custom cards) configured with `gemini-3.7-flash`, and runs the hypervisor.

```text
[Target Directory]
       │
       ▼  (tools/verify_mesh_env)
[Pre-Flight Verification: `mesh` CLI, dependencies, live `pi` or `copilot` probe]
       │
       ▼  (mesh init / tools/mesh_bootstrap)
[Scaffold Layout: .agents/{well_known,skills,workflows,sessions,tasks}]
       │
       ▼  (mesh host --workspace <path>)
[MESH Hypervisor & A2A Endpoints Active @ http://127.0.0.1:<port>]
```

## When to Use This Skill

Use this capability when:
- Bootstrapping a new autonomous agent workspace or project repository.
- Configuring agent topologies (`triad`, `research`, `machine_manager`, or custom agent cards).
- Verifying whether a host system has the prerequisites (`mesh` CLI and functional `pi`/`copilot` execution engines).
- Running pre-flight checks before starting multi-agent orchestrations.

---

## Topology Presets

All presets default to LLM provider `google` and model `gemini-3.7-flash` (thinking effort: `medium`):

1. **`triad`:** Software engineering fleet
   - `orchestrator`: Requirements decomposition, task delegation, and DoD validation.
   - `dev`: Full-stack code implementation, bug fixing, refactoring, and testing.
   - `infra`: Build system automation, test running, and environment enablement.

2. **`research`:** Investigation and synthesis fleet
   - `orchestrator`: Investigation planning and report consolidation.
   - `researcher`: Deep fact gathering, repository exploration, and evidence extraction.
   - `analyser`: Critical evaluation, peer review, and gap synthesis.

3. **`machine_manager`:** Host compute management fleet
   - `node_agent`: Owns the computer's identity, manages capabilities/resources, coordinates local & distributed activities.
   - `execution_worker`: Executes delegated tasks using host resources and tools.

4. **`custom`:** Custom agent cards imported via `--cards <path>`.

---

## Workflow: Bootstrapping a MESH Workspace

### Step 1: Pre-flight Verification
Run the pre-flight verification script to confirm `mesh` CLI and `pi` / `copilot` connectivity:
```bash
tools/verify_mesh_env
```
*Note: If `mesh` CLI is missing or neither `pi` nor `copilot` responds to the probe, bootstrapping pauses with clear installation instructions.*

### Step 2: Bootstrap the Target Workspace
Initialize the target workspace with the chosen topology preset using the `mesh` CLI or the `mesh_bootstrap` helper tool:

**Option A: Multi-Agent Triad Preset**
```bash
mesh_bootstrap /path/to/target_workspace --name "MyProject" --template triad
```
*(Direct `mesh` CLI alternative: `mesh init /path/to/target_workspace --cards .agents/skills/mesh-bootstrapper/templates/triad --model gemini-3.7-flash`)*

**Option B: Research & Analysis Preset**
```bash
mesh_bootstrap /path/to/target_workspace --name "ResearchProject" --template research
```
*(Direct `mesh` CLI alternative: `mesh init /path/to/target_workspace --cards .agents/skills/mesh-bootstrapper/templates/research --model gemini-3.7-flash`)*

**Option C: Machine Manager Preset**
```bash
mesh_bootstrap /path/to/target_workspace --name "NodeHost" --template machine_manager
```
*(Direct `mesh` CLI alternative: `mesh init /path/to/target_workspace --cards .agents/skills/mesh-bootstrapper/templates/machine_manager --model gemini-3.7-flash`)*

### Step 3: Launch the MESH Runtime Hypervisor
Start the hypervisor server using the `mesh host` CLI command:
```bash
mesh host --workspace /path/to/target_workspace --port 8000 --agent all
```

### Step 4: Interact & Verify Status
Inspect cluster telemetry or chat directly with any agent:
```bash
# Check status of cluster and active agents
mesh status --url http://127.0.0.1:8000

# Open interactive chat session with the orchestrator
mesh chat --agent orchestrator --url http://127.0.0.1:8000
```

---

## References

- [references/agent-card-schemas.md](references/agent-card-schemas.md) — Agent card schema and override options.
- [references/topology-presets.md](references/topology-presets.md) — Detailed breakdown of roles and skill sets for `triad`, `research`, and `machine_manager`.
- [references/troubleshooting.md](references/troubleshooting.md) — Operational best practices and troubleshooting.
