# Reference: Topology Presets & Workflow Contracts

In ABB Agent MESH, an agent is modeled cleanly through a **lean system prompt** coupled with a dedicated **Profile ECP**. Profile ECPs encapsulate behavioral methodology, stage responsibilities, delegation rules, and verification standards without bloating the system prompt or relying on hallucinated capabilities.

All presets default to LLM provider `google` and model `gemini-3.7-flash` with thinking effort set to `medium`.

---

## 1. `triad` Preset (Multi-Agent Engineering Fleet)

The standard autonomous software engineering fleet:

- **`orchestrator` (`orchestrator.json`):**
  - **Role:** Lead Workflow Orchestrator and Technical Coordinator. Directs multi-agent lifecycles, plans feature delivery, breaks down requirements, and delegates tasks exclusively to `dev` and `infra` agents via A2A.
  - **Skills:** `a2a-peer-dialing`, `profile-orchestrator`.
- **`dev` (`dev.json`):**
  - **Role:** Full-Stack and Systems Software Engineer. Responsible for feature implementation, code architecture, refactoring, bug fixes, and unit test verification.
  - **Skills:** `a2a-peer-dialing`, `profile-dev`.
- **`infra` (`infra.json`):**
  - **Role:** Infrastructure and Environment Specialist. Responsible for environment provisioning, test suite execution, container operations, VM/network management, and CI/CD automation.
  - **Skills:** `a2a-peer-dialing`, `profile-infra`.

---

## 2. `research` Preset (Investigation & Analysis Topology)

Deep technical discovery, literature review, and evaluation:

- **`orchestrator` (`orchestrator.json`):**
  - **Role:** Research Coordinator and Lead Investigator. Breaks down complex research topics, assigns investigation streams to researcher and analyser agents, and synthesizes final reports.
  - **Skills:** `a2a-peer-dialing`, `profile-orchestrator`.
- **`researcher` (`researcher.json`):**
  - **Role:** Deep Investigation and Evidence Gathering Agent. Scours documentation, source repositories, APIs, and literature to extract facts, patterns, and technical data.
  - **Skills:** `a2a-peer-dialing`, `profile-researcher`.
- **`analyser` (`analyser.json`):**
  - **Role:** Critical Technical Analyser and Synthesis Agent. Evaluates collected research findings, identifies gaps, validates hypotheses, and performs peer review.
  - **Skills:** `a2a-peer-dialing`, `profile-analyser`.

---

## 3. `machine_manager` Preset (Host Control & Local Execution)

Machine management and local execution topology:

- **`node_agent` (`node_agent.json`):**
  - **Role:** Node Agent — Owns the computer's identity, manages its capabilities and resources, and coordinates local and distributed activities.
  - **Skills:** `a2a-peer-dialing`, `profile-node-agent`.
- **`execution_worker` (`execution_worker.json`):**
  - **Role:** Execution Worker — Executes delegated tasks using the resources and capabilities available on the computer.
  - **Skills:** `a2a-peer-dialing`, `profile-execution-worker`.

---

## 4. `custom` Mode

- **Agent Cards:** Loaded directly from custom JSON files or directories via `--cards <path>`.
- **Workflow:** Dynamic collaborative contract auto-generated during `mesh init`.
