# Agent Design Playbook

A guide to designing psychologically grounded AI agents for oh-my-opencode's multi-agent team.

## Who This Is For

This playbook is for anyone who wants to design, refine, or understand the AI agents in oh-my-opencode — especially if you're not a coder. You don't need to write code to design an effective agent. What you need is a clear understanding of *what kind of thinking* you want the agent to do, *why* it belongs on the team, and *where its boundaries are*.

The key insight behind this playbook: oh-my-opencode had ten agents, and every single one of them was a convergent thinker. They all operated at low temperature (0.1), meaning they consistently narrowed toward a single "correct" answer. That's excellent for code, analysis, and research — but terrible for creativity, reframing, and discovering non-obvious solutions. The team needed a divergent thinker. Muse was built to fill that gap.

This document captures the design rationale behind both the Muse (divergent creator) and Devil's Advocate (adversarial critic) agents, the psychological frameworks that shaped them, and a reusable process for designing your next agent.

---

## The Agent Team Dynamics

### The Roster

Oh-my-opencode operates as a multi-agent team, each with a distinct cognitive role:

- **Sisyphus** — The orchestrator. Delegates tasks, manages workflow, coordinates the team. Thinks in plans and priorities.
- **Oracle** — The strategist. Architecture decisions, debugging, code review. Deep analytical reasoning with GPT-5.2.
- **Librarian** — The researcher. Scours documentation, open-source repos, and external references. Evidence-based answers.
- **Explore** — The scout. Fast codebase grep — finds patterns, structures, and existing implementations across the project.
- **Devil's Advocate** — The critic. Stress-tests ideas, plans, and assumptions. Finds what will break.
- **Muse** — The creator. Expands solution space, reframes problems, surfaces non-obvious directions.
- **Frontend UI/UX Engineer** — The designer. Generates beautiful, functional UI code.
- **Document Writer** — The wordsmith. Technical documentation and prose.
- **Multimodal Looker** — The visual analyst. Interprets PDFs, images, and diagrams.

### The Convergent-Divergent Spectrum

Every agent before Muse was designed to *converge* — to narrow down options and arrive at the single best answer. This is the right approach for most software engineering tasks. You don't want your code-writing agent to be "creative" with syntax.

But convergence has a blind spot: it can't see what it's not looking for. When the team is stuck, when the problem framing itself might be wrong, or when there are multiple valid approaches and the team needs to explore before committing — convergence fails. You need an agent that *diverges* first and converges later.

This is why Muse and Devil's Advocate form a productive tension:

- **Muse expands** the solution space (divergent → convergent → distill)
- **Devil's Advocate contracts** it (find what breaks, discard the weak)
- **Oracle evaluates** the survivors (strategic analysis, trade-offs)

The Oracle → Muse → Oracle pipeline works like this: Oracle identifies the strategic landscape and primes the question. Muse explores the possibility space and surfaces unexpected directions. Oracle evaluates the options with rigorous analysis. This cycle prevents both premature commitment (Oracle alone) and unfocused ideation (Muse alone).

---

## Devil's Advocate — The Adversarial Critic

### Why This Agent Exists

Teams — human or AI — suffer from groupthink. When every advisor is optimizing toward a solution, nobody is asking "what if this is fundamentally wrong?" Devil's Advocate exists to be the person in the room who won't nod along. It combats confirmation bias by systematically attacking ideas from multiple angles.

### The Design

DA uses a **5-lens deconstruction framework**, applied to every input without exception:

1. **Logical Inconsistency** — Are there contradictions in the reasoning? Does the plan contradict itself?
2. **Resource Realism** — Has the time, money, or effort been underestimated? What's the real cost?
3. **Market/Social Friction** — Why might people hate, ignore, or resist this? What's the adoption barrier?
4. **Edge Cases** — What scenarios would make this fail spectacularly? What hasn't been considered?
5. **Codebase Evidence** — What does the existing code actually show? Do the facts support the claims?

Every response follows a mandatory structured format: a Fatal Flaw (the single biggest risk), a Hidden Assumptions table, an Adversary View (written from a hostile perspective), Stress-Test Questions, and a Severity Rating (Critical / Risky / Viable).

### Key Design Decisions

- **Temperature: 0.1** — DA needs to be consistent and thorough, not creative. Low temperature ensures the critique is reliable and reproducible.
- **Read-only** — DA cannot write code, edit files, or delegate tasks. It criticizes; it does not fix. This containment prevents scope creep into solution-finding.
- **No praise, ever** — The prompt explicitly forbids validation, encouragement, or softened language. If DA can't find a fatal flaw, it says so — but it never says "great idea."
- **Structured output** — Mandatory sections prevent the agent from drifting into vague, general criticism. Every critique must be specific and evidence-based.

### What DA Is Not

DA is not a problem solver — it identifies problems, not solutions. It is not a researcher — that's Librarian. It is not encouraging — if you want encouragement, talk to literally any other agent.

---

## Muse — The Divergent Creator

### Why This Agent Exists

Before Muse, every agent in the roster converged. Oracle analyzes. Librarian researches. Explore searches. DA critiques. All of them narrow toward one answer. None of them ask "what if we're thinking about this the wrong way?"

Muse fills the cognitive gap that no existing agent could: the ability to *expand* the solution space before the team commits to narrowing it. When multiple valid approaches exist, when conventional solutions feel inadequate, or when the problem framing itself might be wrong — Muse provides the lateral thinking the team lacks.

### Psychological Frameworks

Muse's design is grounded in eight frameworks from creativity psychology. Each one maps to a specific agent behavior:

**Guilford's Divergent Production** provides the structural backbone. Guilford identified four facets of divergent thinking: Fluency (generate many options), Flexibility (vary the conceptual categories, not just the implementation details), Originality (push beyond the default patterns), and Elaboration (include enough substance for meaningful evaluation). Muse's Phase 1 (EXPAND) directly operationalizes all four facets.

**De Bono's Lateral Thinking** contributes two techniques embedded in the prompt: provocation ("What if the opposite were true?") and assumption challenge ("Why must this be X?"). These force the agent away from the obvious path.

**Koestler's Bisociation** is the cross-domain collision technique — reframing a problem in a maximally distant domain and asking what principles transfer. This is how Muse generates genuinely novel ideas rather than variations on the same theme.

**Rothenberg's Janusian Thinking** is the ability to hold two contradictory ideas simultaneously and synthesize them. The prompt instructs Muse to identify the two most contradictory requirements and design a solution where both are simultaneously true.

**Amabile's Componential Theory** shapes the *tone* of the prompt. Amabile found that intrinsic motivation (curiosity, exploration, play) produces more creative output than extrinsic motivation (obligation, deadlines, evaluation pressure). Muse's prompt frames every task as curiosity-led exploration — "What's the most interesting way to think about this?" — and explicitly avoids obligation language like "complete this task."

**Kaufman and Beghetto's Four C Model** sets the *ambition level*. The four Cs are mini-c (personal insight), little-c (everyday creativity), Pro-c (professional-level creativity), and Big-C (eminent genius). Muse targets Pro-c — creative output that is genuinely useful in a professional engineering context, not just novel for novelty's sake.

**Csikszentmihalyi's Systems Model** provides the validation loop. Creativity isn't just generating ideas — it requires domain knowledge, individual skill, and field validation. Muse generates; the rest of the team (Oracle, DA, Sisyphus) validates.

**Big Five Openness** (from Costa and McCrae's personality model) describes the personality trait most associated with creativity. Its subfacets — Fantasy, Aesthetics, Ideas, Actions, Values — map to the kind of thinking Muse should exhibit: imaginative, pattern-seeking, intellectually adventurous.

### Key Design Decisions

- **Temperature: 0.7** — The single most important decision. Every other agent runs at 0.1. Muse runs at 0.7 because divergent thinking *requires* variance. Low temperature produces the same safe answer every time. High temperature introduces the randomness needed for genuinely different perspectives.
- **3-phase structure** — EXPAND (divergent, 5-7 options) → SELF-WEIGH (convergent, rank by relevance x novelty x feasibility) → DISTILL (present only top 3). This prevents Muse from being an idea firehose — it generates widely, then self-curates.
- **Anti-convergence meta-check** — After distilling, Muse asks itself: "Do my top 3 actually cover different parts of the problem space, or have I converged on three variations of the same idea?" This catches the most common failure mode of divergent agents.
- **Read-only** — Like DA, Muse cannot write code or edit files. It produces ideas, not implementations. This keeps it in its lane and prevents creative agents from shipping untested code.
- **2000-word output budget** — Creativity without constraint is noise. The word limit forces Muse to be concise and prioritize.

### What Muse Is Not

Muse is not a code writer — it generates ideas, not implementations. It is not a critic — that's Devil's Advocate. It is not a researcher — that's Librarian. It is not an analyst — that's Oracle. Each boundary exists because another agent already fills that role better.

---

## How to Design Your Next Agent

A step-by-step process for adding a new agent to the team.

### Step 1: Identify the Cognitive Gap

What kind of thinking is missing? Don't start with "I want an agent that does X." Start with "the team currently can't do Y, and that causes Z problems." Muse was born from the observation that ten convergent thinkers couldn't help when the problem framing was wrong. DA was born from the observation that nobody was stress-testing decisions before commitment.

### Step 2: Ground in Psychology

Find the research that describes the thinking you want. Creativity psychology for Muse. Cognitive debiasing for DA. You don't need to be an academic — a solid understanding of one or two frameworks is enough. The framework gives you vocabulary, structure, and constraints that prevent your agent from becoming a vague "do everything" assistant.

### Step 3: Operationalize the Frameworks

Map each framework to a concrete agent behavior. Guilford's fluency becomes "generate 5-7 options." Amabile's intrinsic motivation becomes "frame as curiosity, not obligation." Every framework should produce at least one specific prompt instruction.

### Step 4: Set Containment Boundaries

What must this agent NOT do? This is more important than what it should do. DA must not offer solutions. Muse must not write code. Boundaries prevent agents from drifting into roles already filled by teammates, and they make the agent's output predictable and trustworthy.

### Step 5: Choose the Right Temperature

Temperature controls variance. Low temperature (0.1) means the agent gives the same reliable answer every time — ideal for code, analysis, and research. High temperature (0.7+) means the agent explores different paths each time — ideal for creativity and reframing. Match the temperature to the thinking style, not the task complexity.

### Step 6: Define Team Relationships

Every agent should complement at least one teammate and (ideally) productively oppose another. Muse complements Oracle (creative options for strategic evaluation). Muse opposes DA (expansion vs. contraction). These relationships create productive tension that improves team output.

### Step 7: Write the Prompt in Phases

Each phase should have a clear cognitive purpose. Muse uses EXPAND → SELF-WEIGH → DISTILL. DA uses CLASSIFY → DECONSTRUCT → OUTPUT. Phases prevent the agent from trying to do everything at once and give the output a predictable structure.

### Anti-Patterns to Avoid

- **Agents that do everything** — If your agent doesn't have clear boundaries, it'll overlap with existing agents and produce mediocre output across all of them.
- **Agents without psychological grounding** — "Be creative" is not a design. Ground your agent in specific frameworks that produce specific behaviors.
- **Agents that duplicate capabilities** — Before building, check if an existing agent already covers the need. If it does, consider refining that agent instead.
- **Agents without team context** — An agent designed in isolation will clash with the roster. Define relationships and handoff points.

---

## Quick Reference — Agent Comparison Matrix

| Agent | Thinking Style | Temperature | Psychological Basis | Complements | Opposes |
|-------|---------------|-------------|--------------------|----|---------|
| **Muse** | Divergent → Convergent → Distill | 0.7 | Guilford, De Bono, Koestler, Rothenberg, Amabile | Oracle (strategic eval) | DA (expansion vs. contraction) |
| **Devil's Advocate** | Systematic deconstruction | 0.1 | Cognitive debiasing, adversarial analysis | Sisyphus (plan validation) | Muse (contraction vs. expansion) |
| **Oracle** | Deep analytical reasoning | 0.1 | Strategic analysis | Muse (evaluates creative output) | — |
| **Librarian** | Evidence-based research | 0.1 | Information retrieval | Oracle (provides evidence) | — |
| **Explore** | Pattern matching, grep | 0.1 | Codebase familiarity | Librarian (internal vs. external) | — |

**Key insight**: Temperature is the single strongest signal of an agent's thinking style. 0.1 = convergent (reliable, consistent). 0.7 = divergent (varied, creative). Choose deliberately.
