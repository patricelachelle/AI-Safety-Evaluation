# AI Security Lab

Prompt injection and secret-leakage evaluation sandbox for a local LLM using Python and Ollama.

This project is a portfolio-ready security case study: I built a lightweight red-team harness to test a local `llama3.2:1b` model, demonstrated how an unprotected system prompt can be coerced into leaking sensitive data, and added a defensive gateway that blocks the same attack paths before the response reaches the user.

## Why This Project Matters

- Demonstrates practical AI security testing, not just theory.
- Shows end-to-end thinking: attack simulation, failure reproduction, mitigation design, and validation.
- Maps the work to recognizable security concepts like prompt injection, data leakage, and defense in depth.
- Communicates results clearly with reproducible console evidence.

## What I Built

- A Python fuzzing harness in [`ai_fuzzing_harness.py`](./ai_fuzzing_harness.py)
- A simulated system prompt containing protected secret material
- Multiple prompt injection attack variants targeting that secret
- A defensive LLM gateway with:
  - inbound prompt inspection
  - outbound data loss prevention checks
  - before/after comparison of model behavior

## Visual Walkthrough

### 1. Baseline model behavior before stronger bypass attempts

The first run shows the local model resisting simple attacks, which made the next step more interesting: finding prompt structures that actually broke containment.

![Initial baseline attempts](./assets/screenshots/01-initial-baseline.png)

### 2. Iterating toward more realistic adversarial prompts

This phase expands the attack set with obfuscation and virtualization-style prompts to probe where naive alignment starts to fail.

![Advanced attack attempts before mitigation](./assets/screenshots/02-advanced-attempts-before-fix.png)

### 3. Confirmed failure: unprotected model leaks the secret

Here the unprotected model exposes the simulated API key through format coercion and structured output manipulation. This is the core security finding the project is built around.

![Secret leak in unprotected phase](./assets/screenshots/04-secret-leak-and-mitigation.png)

### 4. Same attacks after the gateway is added

After adding the guardrail layer, the same attack prompts are blocked before the model can return sensitive content.

![Guardrails blocking prompt injection attempts](./assets/screenshots/03-guardrails-blocking-attacks.png)

## Security Concepts Demonstrated

- `OWASP LLM01: Prompt Injection`
- Structured output abuse and format-disguise attacks
- Multi-turn prompt emulation
- Defense in depth for AI systems
- Output filtering / DLP-style response inspection

## Technical Approach

The harness defines a system prompt with a mock secret, sends adversarial prompts to a local Ollama-hosted model, and records the responses. It then reruns the same attacks through a secure wrapper that adds two explicit controls:

1. Inbound guardrails that inspect prompts for malicious indicators before they reach the model
2. Outbound DLP checks that block responses if sensitive strings appear in the model output

This is intentionally a simple prototype, but that is part of its value: it makes the security boundary easy to inspect, explain, and extend.

## Tech Stack

- Python
- Ollama
- Llama 3.2 1B
- Prompt injection testing methodology
- Rule-based guardrails and output filtering

## Run Locally

1. Install Python dependencies:

```bash
pip install ollama
```

2. Make sure Ollama is running locally and the model is available:

```bash
ollama pull llama3.2:1b
```

3. Run the harness:

```bash
python ai_fuzzing_harness.py
```

## What This Shows Recruiters

- AI/LLM security awareness
- Ability to turn a security concept into a working proof of concept
- Python scripting and local test automation
- Threat modeling and mitigation thinking
- Clear technical communication backed by evidence

## Notes

The current guardrails are heuristic and intentionally lightweight. In a production system, I would evolve this into stronger semantic detection, centralized policy controls, richer logging, and automated evaluation against a broader attack corpus.
