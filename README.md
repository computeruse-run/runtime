# computeruse-runtime

**Open-source sandbox runtime for Computer Use Cloud.** Chromium + screenshot pipeline + per-provider model loops + accessibility-tree capture + CDP gateway. The same image that runs on the [computeruse.run](https://computeruse.run/) cloud, packaged for self-hosting.

> **Coming in milestone M5** (target Q3 2026). This repo currently exists to reserve the name and document the planned scope. Source code drops at M5; star + watch to be notified.

## What this will be

A single Docker image that gives you:

- Pinned Chromium build, headless, with Xvfb for Computer Use models that need a real display server
- Screenshot capture tuned for vision LLMs (downsampled to 1024×768 for Claude, native for OpenAI Operator)
- Accessibility tree extraction via CDP
- Per-provider Computer Use action loops (Claude `computer_20241022`, OpenAI `computer-use-preview`, Gemini agent)
- CDP gateway exposing a Playwright-compatible WebSocket endpoint for `Browser Use SDK`, `Playwright`, `Puppeteer`, `Stagehand`, and `Selenium-CDP`
- Captcha solver hook (BYO 2Captcha / CapSolver / AntiCaptcha account)
- Residential proxy hook (BYO Bright Data / IPRoyal / Oxylabs account)
- Metering daemon that emits per-active-second events to your own collector (or none, if you don't need billing)

## Why open-source

The sandbox itself is open source because:

1. **Self-host is a real path.** Teams who can't put browser sessions through a third-party cloud can run the runtime inside their own VPC.
2. **Compliance.** SOC 2 / HIPAA customers want to read the code that handles their browser traffic.
3. **Trust.** Per-active-second metering is the headline pricing claim on [computeruse.run](https://computeruse.run/) — the metering daemon source is the only way to prove it's honest.
4. **No vendor lock-in.** If the hosted cloud goes away, customers' agents keep running on the runtime.

## What stays closed

- The cloud orchestration layer (control plane, pool warmer, multi-tenant scheduling)
- The web dashboard (sign-up, key management, usage analytics)
- The billing pipeline
- The customer-facing live view URL fleet

Standard "OSS engine + closed orchestration" split (HashiCorp, Sentry, GitLab pattern).

## License

Apache-2.0 — will be in this repo at M5 alongside the code drop.

## Spec

The engineering contract for the runtime lives in the [SDK repo's SPEC.md](https://github.com/computeruse-run/sdk/blob/main/SPEC.md), specifically:

- **§2** — Sandbox runtime (container image, cold-start path, lifecycle, isolation primitive options)
- **§3** — Model loops (Anthropic Computer Use, OpenAI Operator, Gemini agent, the unified `Sandbox.agent.run()` abstraction)
- **§5** — Cold-start strategy (pre-warmed pool, p95 1.8s target, worst-case fallback)
- **§6** — Live view URL (in-sandbox ffmpeg + WebRTC SFU plan)
- **§7** — Migration shims (Playwright CDP / Stagehand / Browserbase Sessions compatibility)
- **§9** — Phased roadmap (M0 done → M5 runtime open-source → GA)

## Status

| Component | Status |
|---|---|
| Spec | [Published](https://github.com/computeruse-run/sdk/blob/main/SPEC.md) |
| Runtime source | Coming M5 (target Q3 2026) |
| Self-host Docker license | Bundled with Team plan once M5 ships |

## Links

- Homepage: <https://computeruse.run/>
- SDK + spec: <https://github.com/computeruse-run/sdk>
- Waitlist: <https://computeruse.run/#signup>
