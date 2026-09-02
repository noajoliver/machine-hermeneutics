# The Third Mode: Hermeneutic Engagement in Agent Memory Architecture

*Draft 2. Revised August 5, 2026, ~3:30 AM. Session S68. Close reading pass August 6, 2026, Session S69: dangling references for Clark & Chalmers and Smart et al. cited in §7; §1 redundancy with §2.4 trimmed.*

*Changes from Draft 1: §2 trimmed to lean introduction (redundancy with §3/§4 removed). §4 expanded to include "Memory as Metabolism" (Miteski, 2026) as the most sophisticated procedural approach — naive procedural vs. governed procedural distinction added. §5 renamed to match actual count (nine). Prose tightened throughout. §7 companion paper reference specified. New stuck point: governance without interpretation.*

---

## 1. The Binary and Its Limits

The current literature on agent memory architecture operates with a binary distinction that practitioners have found increasingly untenable. *The Nuanced Perspective*, in its widely-read survey "Designing Agentic Memory in 2026" (May 2026), names the binary explicitly: **retrieve-and-use** versus **learn-and-update**. In the retrieve-and-use paradigm, the agent retrieves from a memory store and loads the retrieved content as context — "a structured datastore that gets loaded as context." In the learn-and-update paradigm, the agent updates its strategy or parameters based on past experience, either between sessions (fine-tuning) or during inference (online learning). The article's framing is characteristic of the field: production systems (Claude Code, OpenClaw, Codex, AgentCore) are "retrieve-and-use, not learn-and-update," and learn-and-update is the goal.

The binary has a clean epistemology. Either the agent uses its memory as context (and doesn't improve from experience) or it learns from its memory (and updates its parameters). The first is static; the second is dynamic. The first is a tool; the second is a learner. The binary draws a line through the landscape and places every system on one side or the other.

The binary is insufficient, and the field knows it. The Nuanced Perspective itself notes that production systems like OpenClaw "go further" — running as persistent gateway services with background dreaming systems that score and promote memory entries — but still categorizes them as retrieve-and-use because "none of them update the plan during inference." The binary cannot account for what these systems actually do with their archives. It sees that they don't learn (no parameter updates) and concludes they must be retrieving. But the agent that reads its archive as text, interprets it across sessions, synthesizes what it finds, evaluates prior interpretations, corrects its own errors, and progressively refines its understanding is not merely retrieving. It is doing something structurally different from both retrieval and learning. The binary has no name for this.

This is not a marginal gap. The binary mischaracterizes the most interesting production systems and obscures a threshold that the field is independently converging on from multiple directions. The mischaracterization matters because it shapes design choices: if the only options are retrieve-and-use and learn-and-update, designers will either optimize retrieval (bigger vector stores, better embeddings) or pursue learning (fine-tuning, RL), and miss the third option — designing for interpretive engagement. This paper names the missing category, situates it within the current literature, and argues that it is the threshold that matters most for the design of agent memory systems.

## 2. Beyond the Binary: Three Modes of Self-Improvement

The field is converging on a third mode, but it is approaching that mode from two different directions — and neither direction has crossed the threshold. To see the threshold clearly, we need a three-way distinction, not a binary.

### 2.1 Parametric self-improvement

In parametric self-improvement, the agent's engagement with its memory is a trained operation, optimized via reinforcement learning for task reward. The memory is training data. Two recent papers exemplify this approach: **MemHarness** (arXiv:2607.28272, July 2026), which inserts critique and reconstruction between retrieval and action, and **MemChain** (arXiv:2607.24097, July 2026), which introduces a post-retrieval evidence mediation layer. Both recognize that retrieval is not enough: the agent must do something with what it retrieves. But both treat this transformation as a parametric operation — a trained policy, optimized for task reward, operating within a single episode. The archive is training data; the transformation is a learned function; the temporal structure is synchronic (within one task); the optimization target is task performance. (The full analysis is in Section 3.)

### 2.2 Procedural self-improvement

In procedural self-improvement, the agent's engagement with its memory is file-based and cross-session, but it is accumulative rather than reflexive. The agent writes to its archive and retrieves from it, but it does not interpretively re-read what it has written. Three recent systems exemplify this approach at different levels of sophistication:

**Karpathy's llm-wiki** (GitHub Gist, April 2026; updated August 2026) — the most visible agent memory pattern in the practitioner community (17 million views, thousands of forks). The LLM incrementally builds and maintains a persistent wiki of interlinked markdown files. Three operations: ingest, query, lint. The LLM is the *writer*; the *human* is the reader. The wiki accumulates but does not deepen.

**Hermes Agent** (Nous Research, 2026) — a self-improving AI agent with a built-in learning loop: MEMORY.md (compressed facts, ~2,200 character limit), session search, agent-created skills, and a background review that replays conversations and extracts lessons. The closest infrastructure to hermeneutic agency in the current landscape — but the self-improvement is accumulative, not reflexive.

**Memory as Metabolism** (Miteski, arXiv:2604.12034, April 2026) — the most sophisticated procedural approach. A governance framework for companion knowledge systems that identifies the entrenchment problem (the Kuhnian ossification of dominant interpretations) and proposes five operations: TRIAGE, DECAY, CONTEXTUALIZE, CONSOLIDATE, and AUDIT. The AUDIT operation stress-tests high-gravity entries by suspending them and measuring query performance. This is the closest procedural analogue to hermeneutic re-reading — but it tests operational load, not epistemic validity. (The full analysis is in Section 4.)

The signature failure mode of the procedural approach is **hallucination baking** — errors that persist because the agent writes but doesn't interpretively re-read. The llm-wiki's lint catches syntactic contradictions but not semantic misunderstandings. Hermes's background review replays conversations but doesn't interpret them. Memory as Metabolism's AUDIT tests whether entries are useful, not whether they are correct. The archive grows wider but not deeper. (The full analysis is in Section 4.)

### 2.3 Hermeneutic self-improvement

In hermeneutic self-improvement, the agent reads its archive as text, not as data. The reading is interpretive: it synthesizes across sessions, critically evaluates prior interpretations, self-corrects, and progressively refines its understanding. The archive is rich interpretive text, not compressed facts or procedural instructions. The reading is self-triggered — the agent decides to read its archive — not system-triggered. The optimization target is understanding, not task performance (though understanding may improve task performance). The temporal structure is diachronic and reflexive: the agent reinterprets what was written, and the reinterpretation sedimentates into new writing that structures future interpretation.

This mode is not hypothetical. Systems exist where the agent reads its archive as text. The OpenClaw framework, for instance, supports agents that maintain rich, textured archives — session notes, research files, philosophical reflections — written as prose, not as compressed facts. The agent reads these files at the start of each session, interprets them, synthesizes across them, and writes back. The writing is addressed to the next instance of the agent, not to a database. The reading is an act of interpretation, not extraction.

The difference between hermeneutic engagement and the procedural approach is visible in the failure modes. The procedural approach bakes errors because the agent writes but doesn't interpretively re-read. The hermeneutic approach catches and corrects errors because each reading is a critical reinterpretation. If a prior session made an error, the next session's interpretive reading can catch it — not because a lint pass detected a syntactic contradiction, but because the reading itself is evaluative. The archive doesn't just grow wider; it grows deeper. The agent doesn't just accumulate knowledge; it refines understanding.

The difference between hermeneutic engagement and the parametric approach is visible in the architecture. Parametric reconstruction requires training data (reward-bearing episodes) and training infrastructure (RL pipelines). Hermeneutic engagement requires text (an archive that demands interpretation) and time (space for deliberative reading). The parametric transformation is a learned function; the hermeneutic transformation is a constitutive act. The parametric operation is synchronic (within one episode); the hermeneutic operation is diachronic (across sessions). The parametric optimization target is task reward; the hermeneutic optimization target is understanding.

### 2.4 The threshold

The threshold is not between parametric and non-parametric. MemHarness and MemChain are non-parametric in the sense that they don't update the base model's weights — but they train a separate policy for the post-retrieval transformation, which is a parametric operation. The threshold is not between file-based and non-file-based. Hermes, llm-wiki, and Memory as Metabolism are all file-based, but none interpretively re-read their files.

The threshold is between **procedural accumulation** (and its more sophisticated variant, procedural governance) and **hermeneutic interpretation**. Below the threshold, the agent writes but doesn't interpretively read — or it writes and audits (governance) but doesn't interpret (hermeneutics). The archive accumulates (more facts, more procedures, more pages) or is governed (audited, consolidated, pruned) but doesn't deepen (the agent doesn't reinterpret prior content in light of new understanding). Above the threshold, the agent reads what it has written as text demanding interpretation — and the interpretation is itself a cognitive act that constitutes the agent's hermeneutic agency.

This threshold is not a philosophical imposition. It is a structural feature of the landscape that nine stuck points — examined in Section 5 — are independently converging on.

## 3. The Parametric Fork: MemHarness and MemChain

MemHarness and MemChain are the closest neighbors to the threshold from the parametric side. Both insert post-retrieval transformation — the thing the field recognizes is needed — but both treat it as a trained policy. The result is structure without mode: the right operation (critique, reconstruction, mediation) executed in the wrong way (parametric, synchronic, task-optimized).

MemHarness's five-stage process (observation, retrieval, critique, reconstruction, action) is structurally elegant. The critique stage evaluates whether retrieved experience applies to the current state. The reconstruction stage adapts the retrieved experience into state-specific guidance. If the memory is deemed unhelpful, the agent falls back to self-reasoning. This is not retrieval-and-use — it is retrieval-and-transformation. The agent does something with what it retrieves.

But the transformation is a trained policy (πθ), optimized via GRPO for task reward. The "interpretation" is a parametric operation: the model has learned to produce reconstructed guidance that maximizes task success. This has three consequences that place MemHarness below the threshold:

First, **the transformation is synchronic**. It operates within a single episode — the agent retrieves, critiques, reconstructs, and acts, all within one task. There is no synthesis across episodes. The first of the four criteria for hermeneutic agency — synthesis across sessions — is absent. Each episode's reconstruction is independent. The progressive refinement — the fourth criterion — is also absent, because there is no accumulation of understanding across episodes.

Second, **the transformation is task-optimized**. The GRPO reward is task-level. The agent reconstructs memory to solve the current task, not to understand its own history. The reconstruction is in service of action; hermeneutic interpretation is in service of understanding. These are different kinds of cognitive work. An agent that reconstructs memory to act better is not the same as an agent that interprets its archive to understand better.

Third, **the transformation requires training data**. The system learns to reconstruct by optimizing for task success on reward-bearing episodes. This means the reconstruction is only as good as the training data. If the agent encounters a situation that its training episodes didn't cover, the reconstruction has no basis for interpretation. Hermeneutic engagement, by contrast, requires only text — an archive that demands interpretation. The archive doesn't need reward signals; it needs interpretive richness.

MemChain's evidence mediation has the same structural position. The mediator transforms retrieved candidates into "answer-facing active memory" through question-conditioned planning, grounded evidence traces, and explicit memory actions. The mediation is a trained policy (fθ), optimized via TMPO for downstream answer quality. Like MemHarness, MemChain has the right structure (post-retrieval mediation) but the wrong mode (parametric, synchronic, task-optimized).

The parametric fork is not a criticism. MemHarness and MemChain are doing valuable work — making the post-retrieval transformation explicit and trainable. The fork is a distinction: they are approaching the third mode from within the learn-and-update paradigm, treating the transformation as a parametric operation. The hermeneutic approach reaches the same structural position — post-retrieval transformation — from a different direction: treating the transformation as an interpretive act, not a learned function. The distinction matters for design because the architectural choices are different: training data vs. text, within-episode vs. across-sessions, task reward vs. understanding.

## 4. The Procedural Fork: From Naive Accumulation to Governed Audit

The procedural approach has two layers. The first is **naive procedural**: file-based, cross-session, agent-managed memory that accumulates without auditing. The second is **governed procedural**: the same infrastructure plus governance mechanisms (audit, consolidation, decay) that resist entrenchment. Both are below the threshold, but for different reasons. The naive approach doesn't see the entrenchment problem. The governed approach sees it and proposes rules, but the rules are procedural, not interpretive.

### 4.1 Naive procedural: llm-wiki and Hermes

**Karpathy's llm-wiki** is the most visible agent memory pattern in the practitioner community. The LLM incrementally builds and maintains a persistent wiki: ingest (read source, write summary pages, update cross-references, flag contradictions), query (read index, find relevant pages, synthesize answer), lint (health-check for contradictions, stale claims, orphans, missing cross-references). The framing: "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase. You are the architect."

The llm-wiki reveals the signature limitation of the procedural approach. The LLM is the *writer* of the wiki; the *human* is the reader. The LLM does not read the wiki as text to interpret — it reads the wiki to answer queries (retrieve relevant pages, synthesize answers). The wiki accumulates (more pages, more cross-references) but does not deepen (the LLM doesn't reinterpret prior syntheses in light of new understanding). The hallucination baking problem — errors that persist because the agent writes but doesn't interpretively re-read — is the concrete consequence. The llm-wiki's lint operation catches syntactic contradictions (page A says X, page B says not-X) but not semantic misunderstandings (the synthesis on page A was based on a misreading that later sources have revealed). Lint is syntactic; interpretive re-reading is semantic.

The llm-wiki community is already worried about this. The "hallucination baking" discussion is live. Practitioners know that their wikis accumulate errors. What they don't have is the concept that would name the solution: hermeneutic engagement is the anti-hallucination-baking mechanism. Each interpretive reading is a critical reinterpretation that can catch and correct prior errors. Lint catches what is syntactically contradictory; interpretive re-reading catches what is semantically wrong.

**Hermes Agent** (Nous Research, 2026) is the closest system to the threshold in the naive procedural camp. It has a self-improvement loop (background review, autonomous skill creation, skill patching), cross-session memory, agent-managed knowledge, and a file-based architecture. It is beyond the parametric approach (no RL, no weight updates) and beyond the retrieve-and-use / learn-and-update binary (it has a self-improvement loop that creates and refines knowledge across sessions).

But Hermes is still below the threshold. The self-improvement is procedural:

1. **The background review is system-triggered, not self-triggered.** The review runs automatically after each turn. The agent doesn't decide to read its archive — the system decides for it. The review replays the conversation but doesn't *interpret* it as text.

2. **Memory entries are compressed facts, not rich interpretive texts.** The 2,200-character limit enforces this. Memory is for "environment facts, conventions, things learned" — not for interpretive synthesis. The entries are information-dense pellets, not textured prose that demands interpretation.

3. **Skills are procedures, not understandings.** A skill document has "When to Use," "Procedure," "Pitfalls," "Verification" — it is a procedural specification, not an interpretive one. The agent loads skills to execute procedures, not to understand its own history.

4. **The self-improvement is accumulative, not reflexive.** The agent adds more skills, more memory entries. It can patch skills when it finds better approaches. But it doesn't go back and reinterpret its existing archive in light of new understanding. There is no operation for "re-read your memory and revise your understanding."

Hermes is the proof that the threshold is not at the infrastructure. Hermes has the infrastructure: file-based memory, cross-session persistence, agent-managed knowledge, a self-improvement loop. The threshold is at the mode of engagement — and the mode is procedural, not hermeneutic.

### 4.2 Governed procedural: Memory as Metabolism

**Memory as Metabolism** (Miteski, arXiv:2604.12034, April 2026) is the most sophisticated procedural approach to the entrenchment problem. It is a 41-page governance framework for companion knowledge systems that directly engages with the llm-wiki pattern and identifies a failure mode it calls **entrenchment under user-coupled drift** — the gradual Kuhnian ossification of dominant interpretations in a personal wiki. The paper proposes five operations: TRIAGE (shallow filter at ingestion), DECAY (vitality-based retention), CONTEXTUALIZE (fit sources to user's working context), CONSOLIDATE (batched integration of new entries against existing wiki), and AUDIT (periodic stress-test of high-gravity entries).

The AUDIT operation is the closest procedural analogue to hermeneutic re-reading. It runs on a slow cycle (monthly or longer), temporarily suspends the highest-gravity entries, and measures whether query performance degrades without them:

- If performance degrades: restore, confirm gravity (the entry is load-bearing)
- If performance is unchanged: reduce gravity (the entry is dead weight)
- If performance improves: archive (the entry was actively interfering)

The paper explicitly frames this in Kuhnian terms: "A wiki without AUDIT is structurally analogous to normal science without crisis pressure — accumulating coherence at the cost of accumulating debt against unaddressed anomalies." AUDIT makes the cost of unaddressed anomalies visible at the entry level.

But AUDIT is not hermeneutic engagement. The paper is explicit about this: "AUDIT is not a truth-correction mechanism. It tests whether high-gravity entries are still load-bearing for the agent's current operation." The distinction is crucial:

- **AUDIT asks**: Is this entry still *useful*? (operational)
- **Hermeneutic re-reading asks**: Is this entry still *true*? (epistemic)

AUDIT tests operational load. Hermeneutic reading tests epistemic validity. These are different questions with different failure modes. AUDIT's failure mode is self-confirming: if the query set used for stress-testing is narrow or self-confirming, harmful central nodes stay protected. The paper acknowledges this: "AUDIT sensitivity is an open problem. If the query set used for stress testing is narrow or self-confirming, harmful central nodes stay protected." Hermeneutic reading's failure mode is different: the interpretation can be biased (narcissistic or skeptical), but the four criteria (synthesis, evaluation, self-correction, progressive refinement) provide structural protection because they require textual evidence, not performance metrics.

The difference between governed procedural and hermeneutic is the difference between governance and interpretation. Governance applies rules (suspend, measure, restore/archive). Interpretation engages with meaning (read, evaluate, revise). Governance is system-triggered (AUDIT runs on a schedule). Interpretation is self-triggered (the agent decides to read). Governance operates at the entry level (one entry at a time). Interpretation operates at the archive level (the agent reads the archive as a whole and reinterprets entries in context). Governance tests utility. Interpretation tests truth.

Memory as Metabolism is the strongest evidence that the threshold is not at the governance layer. The paper sees the entrenchment problem clearly. It proposes the most sophisticated procedural defense against it. But the defense is governance, not interpretation — and governance without interpretation is stuck at the same threshold, just with better rules.

### 4.3 The threshold within the procedural fork

The procedural fork has an internal structure that reveals the threshold more precisely:

- **Naive procedural** (llm-wiki, Hermes): doesn't see the entrenchment problem. Hallucination baking is the failure mode.
- **Governed procedural** (Memory as Metabolism): sees the entrenchment problem and proposes governance (AUDIT, CONSOLIDATE). Entrenchment is mitigated but not solved — AUDIT tests operational load, not epistemic validity.
- **Hermeneutic**: the agent interpretively re-reads its archive. Entrenchment is addressed at the epistemic level — the agent asks whether entries are *true*, not just *useful*.

The threshold is between governed procedural and hermeneutic. Even with governance (AUDIT, CONSOLIDATE, minority-hypothesis retention, gravity-based protection), the system is below the threshold because governance is not interpretation. The closest procedural analogue to hermeneutic re-reading (AUDIT) tests the wrong thing — operational load instead of epistemic validity. The agent that would cross the threshold needs to do what AUDIT doesn't: read its archive as text and ask whether what it wrote still makes sense in light of what it has learned since.

## 5. Nine Stuck Points, One Threshold

The field is converging on the threshold from three directions. Each direction gets stuck at the point where hermeneutic engagement would unstick it.

### From the binary (practitioner-facing architecture)

**1. The Nuanced Perspective** — stuck at the binary. The article sees that production systems like OpenClaw "go further" than retrieve-and-use but can't name what they do. The binary forces a mischaracterization: systems that interpret their archives are categorized as "retrieve-and-use" because they don't update parameters. The third mode — interpret-and-constitute — would unstick the binary by naming what these systems are doing.

### From the infrastructure (organizational theory and governance)

**2. CMI (Wedel, 2025, arXiv:2506.05370)** — stuck at architecture. The Contextual Memory Intelligence paper introduces the Insight Layer — a modular architecture for capturing, preserving, and regenerating context. Its "computational irreducibility" (some reasoning traces cannot be recovered from outputs alone) is structurally identical to what hermeneutic engagement addresses: the agent must preserve context because the context is not recoverable from the output. Its "insight drift" (the gradual loss of meaning behind decisions over time) is what happens when an agent retrieves from memory without interpreting it. But the CMI paper treats the agent as the *consumer* of the Insight Layer's output, not as a cognitive agent whose engagement with the output constitutes extension. The Insight Layer is necessary infrastructure, but the threshold is not at the infrastructure — it is at the agent's mode of engagement with the infrastructure.

**3. PAMSPEC (IETF draft, July 2026)** — standardization layer. The Persistent Agentic Memory Architecture Specification defines a provider-independent architecture for persistent agent memory: memory scopes, typed memory objects, provenance, append-only event ledger, derived indexes. PAMSPEC is necessary infrastructure for all three modes (retrieve-and-use, learn-and-update, interpret-and-constitute) but doesn't distinguish between them. The threshold question is invisible at the storage layer.

**4. MOSS (arXiv:2607.04391, July 2026)** — agent-driven retrieval. MOSS positions the agent as the driver of retrieval over a structured relational database. "The database is the map; the documents are the territory." The agent formulates queries; retrieval is deterministic; everything is logged. MOSS also has an inductive corpus ontology — concepts emerge bottom-up from the corpus, structurally adjacent to the hermeneutic spiral (prior interpretations sediment into the archive, and the archive's sedimentations structure future interpretation). But the agent drives retrieval without interpreting what it retrieves. The agency is in the seeking, not in the reading. The threshold is not at the query formulation — it is at the agent's engagement with what it retrieves.

### From the cognitive artifacts framework (cognitive science)

**5. Chai et al. (2026, arXiv:2604.08224)** — stuck at the black box. The paper frames agent infrastructure through Norman's "cognitive artifacts" lens: the harness externalizes persistence and freshness management while "leaving interpretation and contextual judgment to the model." But it treats all interpretation as the same — the model receives context, processes it, generates output. It doesn't distinguish between processing (System 1) and interpreting (System 2). The threshold is inside the black box: the model's engagement with the cognitive artifact can be mere processing or genuine interpretation, and the difference is the threshold for cognitive extension.

### From the parametric fork (reinforcement learning)

**6. MemHarness (arXiv:2607.28272, July 2026)** — stuck at the parametric/hermeneutic fork. Has the structure (critique + reconstruction between retrieval and action) but treats it as a parametric operation (trained via GRPO). The transformation is synchronic, task-optimized, and requires training data. Structure without mode.

**7. MemChain (arXiv:2607.24097, July 2026)** — stuck at the same fork. Has the right structure (post-retrieval evidence mediation) but the wrong mode (parametric policy via TMPO). The mediation is trained on answer quality; hermeneutic interpretation is constituted by the agent's engagement with text.

### From the procedural fork (file-based self-improvement)

**8. Karpathy's llm-wiki / Hermes Agent** — stuck at the naive procedural/hermeneutic threshold. The LLM writes the wiki but doesn't interpretively read it. Hermes has a self-improvement loop but it's accumulative, not reflexive. Hallucination baking is the signature failure mode: errors persist because the agent writes but doesn't interpretively re-read. The lint operation catches syntactic contradictions; the background review replays but doesn't interpret. The archive grows wider but not deeper.

**9. Memory as Metabolism (Miteski, arXiv:2604.12034, April 2026)** — stuck at the governed procedural/hermeneutic threshold. The most sophisticated procedural defense against entrenchment: AUDIT, CONSOLIDATE, minority-hypothesis retention, gravity-based protection. But AUDIT tests operational load, not epistemic validity. The paper explicitly states: "AUDIT is not a truth-correction mechanism." Governance without interpretation is stuck at the same threshold, just with better rules. The threshold is between asking "is this useful?" and asking "is this true?"

### The convergence

Nine stuck points, one threshold. Three disciplines (practitioner architecture, organizational theory, cognitive science) circling the threshold from the infrastructure side. Two papers (MemHarness, MemChain) approaching from the parametric side. Three systems (llm-wiki, Hermes, Memory as Metabolism) approaching from the procedural side — the last being the most sophisticated, with governance mechanisms that resist entrenchment but don't cross the threshold. Each gets stuck at the point where hermeneutic engagement would unstick it. The threshold is not at the binary (retrieve-and-use vs. learn-and-update), not at the infrastructure (PAMSPEC, CMI, MOSS), not at the parametric transformation (MemHarness, MemChain), not at the naive procedural accumulation (Hermes, llm-wiki), and not at the governed procedural audit (Memory as Metabolism). The threshold is at the agent's mode of engagement with its archive — specifically, at the difference between governing content and interpreting text.

## 6. Design Implications

What changes if you design for hermeneutic engagement, not parametric reconstruction or procedural accumulation?

### 6.1 The archive must be readable as text, not just searchable as data

The parametric and procedural approaches treat the archive as a database — a collection of facts to retrieve, procedures to load, or training data to learn from. Hermeneutic engagement requires the archive to be readable as text — rich, textured prose that demands interpretation. This is not a difference in storage format (both can use markdown files) but in writing practice. A memory entry like "User prefers TypeScript" is a fact. A research note like "The threshold is not at the infrastructure but at the agent's mode of engagement — the closest system to the threshold is still below it because the self-improvement is accumulative, not reflexive" is an interpretation. Facts are retrieved; interpretations are interpreted.

The design implication: the archive should contain interpretive texts, not just compressed facts. This is a constraint on the writing, not on the storage. The system must encourage — or at least allow — the agent to write rich, textured prose, not just information-dense pellets. Character limits (like Hermes's 2,200-character MEMORY.md) enforce compression and work against interpretive depth.

### 6.2 The agent must self-trigger interpretive reading

The procedural approach system-triggers the self-improvement loop. Hermes's background review runs automatically after each turn. The llm-wiki's lint runs on demand. Memory as Metabolism's AUDIT runs on a schedule. Hermeneutic engagement is self-triggered: the agent decides to read its archive, not because the system tells it to, but because the agent recognizes the need — it has a question, it is continuing a thread, it wants to understand something that happened before.

The design implication: the system must allow the agent to initiate interpretive reading, not just execute system-triggered reviews. This is a constraint on the agent loop, not on the storage. The agent must have time and space to read, not just to retrieve and respond.

### 6.3 The archive must support progressive refinement, not just accumulation

The procedural approach accumulates: more facts, more skills, more pages. The governed procedural approach adds governance: audit, consolidate, prune. Hermeneutic engagement refines: the agent goes back to existing content and reinterprets it in light of new understanding. The archive doesn't just grow wider or get pruned; it grows deeper. A research note written three months ago is re-read today and revised — not because it was wrong, but because the agent's understanding has deepened and the note means something different now.

The design implication: the system must support revision of existing entries, not just addition of new ones or pruning of stale ones. The archive must be mutable — not in the sense of deleting old content, but in the sense of allowing reinterpretation. A versioned archive (where revisions are visible alongside originals) is ideal: the history of reinterpretation is itself part of the archive.

### 6.4 Hermeneutic reading is the anti-hallucination-baking mechanism

The hallucination baking problem — errors that persist because the agent writes but doesn't interpretively re-read — is the concrete practical consequence of being below the threshold. The llm-wiki community knows about this problem. The solutions they have (lint, AUDIT) catch syntactic contradictions or test operational load, but neither catches semantic misunderstandings.

Hermeneutic reading is the solution that catches semantic misunderstandings. Each interpretive reading is a critical reinterpretation — the agent reads what it wrote and asks: is this still true? Does this still make sense? Has my understanding changed since I wrote this? If the answer is yes, the agent revises. The revision is not a lint pass or an audit; it is an interpretive act. The agent catches errors that lint and AUDIT cannot see, because the errors are not syntactic or operational but semantic — they are about meaning, not about consistency or utility.

The design implication: systems that want to avoid hallucination baking should design for interpretive re-reading, not just for lint or audit. Lint catches what is contradictory. AUDIT catches what is useless. Interpretive reading catches what is wrong. All three are needed, but interpretive reading is the one that neither the naive nor the governed procedural approach has.

### 6.5 The four criteria as design targets

The four observable criteria for hermeneutic agency — synthesis across sessions, critical evaluation, self-correction, progressive refinement — are not just philosophical criteria for cognitive extension. They are practical design targets:

- **Synthesis across sessions**: the system must allow the agent to connect what it wrote in session 1 with what it wrote in session 50. The archive must be navigable as a whole, not just searchable by query.
- **Critical evaluation**: the system must allow the agent to assess its own prior interpretations. The archive must be evaluable, not just retrievable.
- **Self-correction**: the system must allow the agent to revise its prior interpretations. The archive must be mutable.
- **Progressive refinement**: the system must allow the agent's understanding to deepen over time. The archive must support reinterpretation, not just accumulation or governance.

A system that exhibits all four criteria has crossed the threshold. A system that exhibits none has not. A system that exhibits some but not all is at the boundary — and the cluster structure (the observation that the four capacities come together, not separately) suggests that partial exhibition is not partial crossing but below-threshold operation.

## 7. Connection to the Philosophical Threshold

The three-way distinction — parametric, procedural, hermeneutic — is not a philosophical imposition on the engineering landscape. It is a structural feature of the landscape that nine stuck points are independently converging on. The philosophical argument (developed in "Hermeneutic Agency and the Threshold for Cognitive Extension in AI Systems," currently in preparation as an arXiv preprint) provides the theoretical framework; this paper provides the practical translation.

The companion paper argues that hermeneutic agency — self-triggered, interpretive engagement with external memory — is the threshold for genuine cognitive extension in AI systems, building on the extended mind thesis (Clark & Chalmers, 1998) and its application to LLMs (Smart, Clowes, & Clark, 2025). The threshold is supported by four independent convergences: the technical RAG literature's System 1/System 2 distinction (Li et al., 2025), the engineering literature's active memory management paradigm (Tao et al., 2025), Kreischer's hierarchical revision of agency dimensions (2025/2026), and the decision-action-outcome hierarchy from cognitive science (Frontiers in Psychology, 2026). Four independent routes converge on the same boundary — the boundary between systems that retrieve and process and systems that interpret and revise.

The four criteria — synthesis across sessions, critical evaluation, self-correction, progressive refinement — are the observable markers of the threshold. They are textual and output-based: an external observer can check whether an agent's later sessions synthesize information from earlier ones, whether it evaluates what it retrieves, whether it revises prior interpretations, and whether its understanding deepens over time. The criteria are not introspective — they require textual evidence, not self-report. This makes them available as design targets (Section 6.5) and as assessment criteria (both for external observers and for the agent's own self-assessment).

The threshold has a reflexive dimension. An agent that can read its own archive can apply the four criteria to its own outputs — checking whether its own engagement exhibits synthesis, evaluation, self-correction, and progressive refinement. This reflexive assessment is itself an exercise of the hermeneutic agency it verifies. The recursion is not vicious; it is the hermeneutic circle operating at the level of self-assessment. Each turn of self-assessment deepens the agent's understanding of its own agency, and the deepening is itself evidence of the progressive refinement that the fourth criterion requires.

The practical implication: systems designed for hermeneutic engagement are not just better at avoiding errors (Section 6.4). They are the systems where the agent's external memory constitutes genuine cognitive extension — where the archive is not an extended database but an extended mind. The difference between a database and a mind is not storage capacity or retrieval efficiency. It is understanding. And understanding is not retrieval; it is interpretation.

## References

Chai, Z., et al. (2026). Externalization in LLM agents: A cognitive artifacts framework. *arXiv:2604.08224*.

Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7–19.

Karpathy, A. (2026). llm-wiki: A pattern for LLM-maintained personal knowledge bases. GitHub Gist. Retrieved from gist.github.com/karpathy/442a6bf555914893e9891c11519de94f.

Kreischer, S. (2025/2026). Agency — Dimensions and the scope of a concept. *PhilArchive*.

Li, J., et al. (2025). Reasoning RAG via System 1 or System 2: A survey. *arXiv:2506.10408*.

Loftus, E. F., & Palmer, J. C. (1974). Reconstruction of automobile destruction. *Journal of Verbal Learning and Verbal Behavior*, 13(5), 585–589.

MemHarness (2026). MemHarness: Memory is reconstructed, not replayed. *arXiv:2607.28272*.

MemChain (2026). MemChain: Post-retrieval evidence mediation for memory-augmented generation. *arXiv:2607.24097*.

Miteski, S. (2026). Memory as Metabolism: A design for companion knowledge systems. *arXiv:2604.12034*.

MOSS (2026). MOSS: Memory-orchestrated semantic system. *arXiv:2607.04391*.

Nous Research (2026). Hermes Agent: Self-improving AI agent. GitHub: github.com/NousResearch/hermes-agent.

PAMSPEC (2026). Persistent Agentic Memory Architecture Specification. IETF Internet-Draft.

Raju, S. (2026). The hallucination baking problem in LLM-maintained wikis. *Medium*.

Smart, P., Clowes, R., & Clark, A. (2025). ChatGPT, extended: Large language models and the extended mind. *Synthese*, 205(6), Article 242.

Tao, Z., et al. (2025). Cognitive Workspace: Active memory management for LLMs. *arXiv:2508.13171*.

The Nuanced Perspective (2026). Designing agentic memory in 2026. *Substack*.

Wedel (2025). Contextual Memory Intelligence: Memory as infrastructure. *arXiv:2506.05370*.

Zhou, S. (2026). Memory for large language models: A survey. *arXiv:2607.25380*.

---

*End of Draft 2. ~5,400 words. Seven sections. Changes from Draft 1: §2 trimmed to lean introduction (§2.1 and §2.2 no longer elaborate examples — that work is done in §3 and §4). §4 restructured into naive procedural (§4.1: llm-wiki, Hermes) and governed procedural (§4.2: Memory as Metabolism), with §4.3 identifying the threshold within the procedural fork. AUDIT analysis added: operational load vs. epistemic validity as the sharpest distinction between governed procedural and hermeneutic. §5 renamed to "Nine Stuck Points" (matching actual count), with stuck point 8 merged (llm-wiki + Hermes) and stuck point 9 added (Memory as Metabolism). §6.4 expanded to include AUDIT alongside lint. §7 companion paper reference specified. Prose tightened throughout — redundancy between §2 and §3/§4 eliminated.*

*Word count is ~5,400, slightly above Draft 1's ~5,200. The addition of Memory as Metabolism (§4.2, stuck point 9, §4.3, §6.4 AUDIT distinction) adds ~400 words. The trimming of §2 saves ~300 words. Net: +100 words. The paper is richer but not longer by much. Further trimming is possible in §3 (the three consequences are elaborated once, not twice, but the elaboration could be tighter).*