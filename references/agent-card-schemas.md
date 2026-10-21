# Reference: Agent Card Schemas & Overrides

This reference describes the agent card schema used by ABB Agent MESH to instantiate autonomous agents.

## Schema Location
Agent cards reside under `<workspace>/.agents/well_known/<agent_name>.json`.

## Standard Fields

| Field | Type | Description |
|---|---|---|
| `name` / `agent_id` | `str` | Unique identifier of the agent within the MESH cluster. |
| `description` | `str` | Human/LLM-readable summary of the agent's capabilities and role. |
| `harness` | `str` | Harness engine adapter: `"pi"`, `"copilot"`, or `"sdk"`. |
| `provider` | `str` | Inference provider: `"google"`, `"anthropic"`, `"openai"`, `"openrouter"`, `"deepseek"`, `"ollama"`, or `"custom-openai"`. |
| `model` | `str` | Specific LLM model string (e.g. `"gemini-2.5-flash"`, `"claude-3-7-sonnet-20250219"`, `"gpt-4o"`). |
| `thinking` | `str` | Reasoning effort: `"off"`, `"minimal"`, `"low"`, `"medium"`, `"high"`, `"xhigh"`, `"max"`. |
| `system_prompt` | `str` | System prompt defining behavioral invariants, operational scope, and role expectations. |
| `skills` | `list[str]` | List of ECP capabilities required by this agent. Deployed to `<workspace>/.agents/skills/`. |
| `base_url` | `str` | (Optional) Custom API endpoint base URL (e.g., `http://localhost:11434/v1`). |
| `api_key_env` | `str` | (Optional) Custom environment variable name holding the API key. |

## Example: Pi Agent Card
```json
{
  "name": "dev_agent",
  "description": "Primary software engineering agent responsible for implementation, debugging, and testing.",
  "harness": "pi",
  "provider": "google",
  "model": "gemini-2.5-flash",
  "thinking": "medium",
  "skills": [
    "a2a-peer-dialing",
    "dev-code-ops"
  ],
  "system_prompt": "You are dev_agent, the core developer in ABB Agent MESH. Follow workflow contracts strictly."
}
```

## Example: Echo Agent Card (Zero-Token Testing)
```json
{
  "name": "echo_agent",
  "description": "Deterministic echo test agent for verification without LLM cost.",
  "class_path": "mesh.agents.echo_agent.EchoAgent"
}
```
