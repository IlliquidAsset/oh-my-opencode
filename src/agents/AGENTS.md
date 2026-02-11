# AGENTS KNOWLEDGE BASE

## OVERVIEW

9 AI agents for multi-model orchestration. Sisyphus orchestrates, specialists handle domains.

## STRUCTURE

```
agents/
├── sisyphus.ts              # Primary orchestrator (504 lines)
├── oracle.ts                # Strategic advisor
├── librarian.ts             # Multi-repo research
├── explore.ts               # Fast codebase grep
├── frontend-ui-ux-engineer.ts  # UI generation
├── document-writer.ts       # Technical docs
├── multimodal-looker.ts     # PDF/image analysis
├── devils-advocate.ts       # Adversarial validation
├── muse.ts                  # Divergent creativity
├── muse.test.ts             # Muse agent tests
├── sisyphus-prompt-builder.ts  # Sisyphus prompt construction
├── build-prompt.ts          # Shared build agent prompt
├── plan-prompt.ts           # Shared plan agent prompt
├── types.ts                 # AgentModelConfig interface
├── utils.ts                 # createBuiltinAgents(), getAgentName()
└── index.ts                 # builtinAgents export
```

## AGENT MODELS

| Agent | Model | Fallback | Purpose |
|-------|-------|----------|---------|
| Sisyphus | anthropic/claude-opus-4-6 | - | Orchestrator with extended thinking |
| oracle | openai/gpt-5.2 | - | Architecture, debugging, review |
| librarian | anthropic/claude-sonnet-4-5 | google/gemini-3-flash | Docs, GitHub research |
| explore | opencode/grok-code | gemini-3-flash, haiku-4-5 | Contextual grep |
| frontend-ui-ux-engineer | google/gemini-3-pro-preview | - | Beautiful UI code |
| document-writer | google/gemini-3-pro-preview | - | Technical writing |
| multimodal-looker | google/gemini-3-flash | - | Visual analysis |
| devils-advocate | google/gemini-3-pro-preview | - | Adversarial validation |
| muse | google/gemini-3-pro-preview | - | Divergent creativity |

## MODEL NOTES

### xAI Grok Model Landscape (Feb 2026)

The Grok model family has evolved significantly. If you have `xai/grok-2-1212` in your configuration, **update immediately** to a newer model.

| Model | Status | Recommended For |
|-------|--------|-----------------|
| `grok-2-1212` | **DEPRECATED** | Nothing — replace immediately |
| `grok-3` | Stable | General reasoning (131K context) |
| `grok-3-mini` | Stable | Lightweight tasks |
| `grok-4` | Latest flagship | Advanced reasoning (256K context) |
| `grok-4-fast` | Latest fast | Reasoning + speed (2M context) |
| `grok-4-1-fast` | **Newest** | Agentic tool calling (2M context) |
| `grok-code-fast` | Current | Coding-specific (256K context) |

**Migration Guide**: If your config uses `xai/grok-2-1212`, replace it with:
- `xai/grok-code-fast` for coding tasks (recommended for `explore` agent)
- `xai/grok-4-1-fast` for general reasoning and tool calling
- `xai/grok-3` for lightweight tasks with lower latency

## HOW TO ADD

1. Create `src/agents/my-agent.ts`:
   ```typescript
   export const myAgent: AgentConfig = {
     model: "provider/model-name",
     temperature: 0.1,
     system: "...",
     tools: { include: ["tool1"] },
   }
   ```
2. Add to `builtinAgents` in index.ts
3. Update types.ts if new config options

## MODEL FALLBACK

`createBuiltinAgents()` handles fallback:
1. User config override
2. Installer settings (claude max20, gemini antigravity)
3. Default model

## ANTI-PATTERNS

- High temperature (>0.3) for code agents
- Broad tool access (prefer explicit `include`)
- Monolithic prompts (delegate to specialists)
- Missing fallbacks for rate-limited models
