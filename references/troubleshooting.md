# Reference: Troubleshooting & Operational Best Practices

## 1. Subprocess Event Loop Compatibility (Windows)
On Windows, async subprocesses (`asyncio.create_subprocess_exec`) require the Proactor event loop. MESH automatically configures `asyncio.WindowsProactorEventLoopPolicy` on Windows hosts.

## 2. API Key Resolution
Ensure target environment keys are set before launching `mesh host`:
```bash
export GEMINI_API_KEY="your-key-here"
# or ANTHROPIC_API_KEY, OPENAI_API_KEY, OPENROUTER_API_KEY
```
Or define them in `<workspace>/.env`.

## 3. Workspace Port Conflicts
By default, MESH listens on port `8000`. To run multiple instances simultaneously or avoid conflicts:
```bash
mesh host --workspace ./my_workspace --port 8010
```

## 4. Bounded Context Protection
To prevent context explosion across agents:
- Never read `.agents/sessions/*.jsonl` files directly from within an agent loop.
- Use `a2a_peer_call` for cross-agent communication.
- Inspect telemetry via `a2a_peer_call status` or bounded logs in `.agents/tasks/`.
