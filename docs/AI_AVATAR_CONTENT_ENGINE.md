# AI Avatar Content Engine

Goal: produce up to 13 short-form AI-avatar posts per day with a human approval gate.

## Architecture

1. Topic planner generates the next approved content slot.
2. Script generator creates a short vertical-video script.
3. Voice layer uses VibeVoice Realtime 0.5B for research/testing.
4. Video layer calls Google Veo via Gemini API for programmable generation.
5. Optional manual refinement happens in Google Flow.
6. Approval queue requires APPROVE / REJECT / REGENERATE before publishing.
7. Publisher adapters send approved assets to supported social platforms.
8. Content ledger records topic, script hash, render ID, status, platform IDs, and metrics.

## Important constraints

- The original VibeVoice 1.5B TTS installation/usage is disabled in the upstream repository.
- VibeVoice Realtime 0.5B is the currently runnable TTS path in this fork.
- The upstream project warns against commercial/real-world deployment without further testing.
- Google Flow is treated as a creative workspace, not the automation API.
- Automated video generation should use the supported Gemini/Veo API.
- Do not publish synthetic media without review.
- Disclose AI-generated content where platform rules or context require it.
- Never clone or impersonate another person's voice without permission.

## Daily pipeline

Each item moves through:
DRAFT -> SCRIPTED -> VOICED -> RENDERED -> REVIEW -> APPROVED -> SCHEDULED -> PUBLISHED -> MEASURED

Rejected items move to REGENERATE or ARCHIVED.

## Production target

13 posts/day is a ceiling, not a quality requirement. The engine should skip a slot rather than publish duplicate, weak, misleading, or low-confidence content.

## Next engineering steps

- Add content planner and duplicate-topic protection.
- Add VibeVoice service wrapper.
- Add Veo video-generation adapter.
- Add approval queue.
- Add publisher adapters.
- Add metrics ingestion.
- Add audit logging and kill switch.
