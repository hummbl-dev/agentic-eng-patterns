# Prior Art and Adjacent Ecosystem

This document collects public prior art and adjacent ecosystem references for
agentic engineering patterns. It closes issue #2.

## Non-canon note

Listing a project here is a **reference**, not an endorsement, adoption, or
canonization. This repository does not claim ownership of any term, pattern, or
concept named below. Vocabulary is used descriptively. Any future canonization
must go through a reviewed governance path and carry an explicit, audited marker
in the artifact and the receipt.

All links point to public documentation or repositories.

---

## Public prior art

These projects are direct prior art for building agentic systems: they provide
agent runtimes, multi-agent orchestration, or opinionated agent abstractions.

### LangGraph

- **What it does:** A library for building stateful, multi-actor systems with
  LLMs using graphs of nodes and edges. Models agent workflows as explicit
  state machines with cycles, branching, and persistence.
- **Relevance:** Direct prior art for orchestration and agent topology. The
  graph-as-control-flow model is a strong reference for how
  `agentTopology` and `errorRecoveryPolicy` can be represented explicitly.
- **Docs:** https://langchain-ai.github.io/langgraph/

### CrewAI

- **What it does:** A framework for orchestrating role-playing autonomous AI
  agents around tasks. Agents have roles, goals, backstories, and tools, and
  collaborate via a crew.
- **Relevance:** Direct prior art for delegation and multi-agent patterns. The
  role/task/tool decomposition maps cleanly onto a packet's
  `patternManifest` and `toolSpecs`.
- **Docs:** https://docs.crewai.com/

### AutoGen

- **What it does:** Microsoft's framework for building multi-agent conversations
  and workflows. Agents converse, call tools, and terminate via configurable
  conditions.
- **Relevance:** Direct prior art for multi-agent conversation, handoff, and
  termination policies. Relevant to `humanInTheLoopPolicy` and
  `errorRecoveryPolicy`.
- **Docs:** https://microsoft.github.io/autogen/

### OpenAI Swarm

- **What it does:** An educational, lightweight framework demonstrating
  multi-agent orchestration via routines and handoffs between agents.
- **Relevance:** Direct prior art for the **handoff** vocabulary and for
  modeling delegation as an explicit primitive. Minimal and readable; a good
  reference for keeping the v0.1 schema small.
- **Docs:** https://github.com/openai/swarm

### AutoGPT

- **What it does:** An early autonomous agent that plans, executes, and
  self-reviews against a high-level goal, using tools and long-term memory.
- **Relevance:** Direct prior art for agent loops, planning, and long-term
  memory. Also a cautionary reference for error recovery and goal drift.
- **Docs:** https://github.com/Significant-Gravitas/AutoGPT

### BabyAGI

- **What it does:** A minimal task-driven agent that creates, reprioritizes,
  and executes tasks in a loop.
- **Relevance:** Direct prior art for the **planning** loop and task
  reprioritization. A useful minimal reference for `patternType` values
  like `plan-and-execute`.
- **Docs:** https://github.com/yoheinakajima/babyagi

### Agno

- **What it does:** A framework for building multimodal agents with memory,
  tools, and structured reasoning, formerly known as Phidata.
- **Relevance:** Direct prior art for memory specs and tool calling patterns.
  Relevant to `memorySpecs` and `toolSpecs`.
- **Docs:** https://docs.agno.com/

### Pydantic AI

- **What it does:** A framework for building agents with strongly typed
  tools and structured outputs, built on Pydantic.
- **Relevance:** Direct prior art for typed tool contracts and structured
  agent I/O. Relevant to `toolSpecs` and the packet's contract framing.
- **Docs:** https://ai.pydantic.dev/

### Semantic Kernel

- **What it does:** Microsoft's SDK for integrating AI services with
  conventional programming via plugins, functions, and planners.
- **Relevance:** Direct prior art for planning and tool-calling in an
  enterprise SDK context. Relevant to `patternType` and `toolSpecs`.
- **Docs:** https://learn.microsoft.com/en-us/semantic-kernel/

---

## Adjacent ecosystem

These projects are not primarily agent runtimes but are adjacent and relevant:
they shape prompting, evaluation, retrieval, structured I/O, and developer
ergonomics that agentic systems depend on.

### DSPy

- **What it does:** A framework for programming LLM pipelines declaratively
  and optimizing prompts via compilation.
- **Relevance:** Adjacent reference for prompt-as-code and for separating
  declarative intent from execution. Relevant to how a packet describes
  contracts without embedding prompt strings.
- **Docs:** https://dspy.ai/

### BAML

- **What it does:** A schema-first language for defining LLM functions and
  extracting structured data with type safety and testing.
- **Relevance:** Adjacent reference for schema-first LLM I/O and testability.
  Relevant to the packet's contract and fixture philosophy.
- **Docs:** https://docs.boundaryml.com/

### LangChain

- **What it does:** A broad framework for building LLM applications with
  chains, agents, tools, and integrations.
- **Relevance:** Adjacent reference for the tool-calling and retrieval
  primitives that underpin many agent loops.
- **Docs:** https://python.langchain.com/

### LlamaIndex

- **What it does:** A framework for data ingestion, indexing, and retrieval
  for LLM applications, including agent and workflow abstractions.
- **Relevance:** Adjacent reference for retrieval-augmented memory and
  long-term memory patterns.
- **Docs:** https://docs.llamaindex.ai/

### Promptfoo

- **What it does:** A CLI and library for testing and evaluating LLM prompts
  and agent behavior against assertions and metrics.
- **Relevance:** Adjacent reference for evaluation and regression testing of
  agent behavior. Relevant to the packet's reviewable, testable posture.
- **Docs:** https://www.promptfoo.dev/

### Instructor

- **What it does:** A library for structured LLM outputs via Pydantic-style
  schemas, with retries and validation.
- **Relevance:** Adjacent reference for structured outputs and retry/error
  recovery on malformed model output. Relevant to `errorRecoveryPolicy`.
- **Docs:** https://instructor.ai/

### Marvin

- **What it does:** A toolkit for building AI-powered functions and agents
  with a focus on developer ergonomics and structured outputs.
- **Relevance:** Adjacent reference for ergonomic agent abstractions and
  function-as-tool patterns.
- **Docs:** https://marvin.ai/

---

## Vocabulary

The following terms are used descriptively in this repository. They are not
proprietary definitions and are not canonized here.

- **agent** — An entity that perceives, decides, and acts, typically by
  calling tools or other agents within a loop.
- **tool** — A callable capability exposed to an agent, with a defined input
  and output contract.
- **planning** — Producing, ordering, or revising a set of steps before or
  during execution.
- **reflection** — Reviewing prior steps or outputs to inform the next action.
- **memory** — State retained across steps or runs; may be short-term,
  long-term, or episodic.
- **delegation** — One agent assigning a task or sub-goal to another agent or
  tool.
- **orchestration** — Coordinating the order, handoffs, and termination of
  agents and tools.
- **multi-agent** — A system with more than one agent role operating
  concurrently or in sequence.
- **handoff** — Transferring control and context from one agent to another.

---

## Key concepts

These are the recurring concepts the v0.1 schema and examples are designed to
accommodate. They are descriptive, not normative.

### Agent loops

A control structure in which an agent observes state, decides an action,
executes it, and repeats until a termination condition is met. The basic
shape underlying most prior art above.

### Tool calling

Agents invoke tools with typed inputs and consume typed outputs. The packet's
`toolSpecs` captures the tool contracts a pattern depends on.

### Planning patterns

- **ReAct** — Interleaved reasoning and acting steps.
- **Plan-and-Execute** — Produce a plan, then execute steps, optionally
  revising the plan.
- **Reflexion** — Reflect on outcomes and feed reflections back into the next
  attempt.

### Memory patterns

- **Short-term** — State within a single run or session.
- **Long-term** — State persisted across runs.
- **Episodic** — Records of past interactions reused as context.

### Delegation patterns

One agent hands a sub-goal to another agent or tool, often with a defined
return contract. Handoff is a specialization of delegation focused on
transferring control.

### Error recovery

Policies for handling tool failures, malformed outputs, timeouts, and goal
drift. Captured in the packet's `errorRecoveryPolicy`.

### Human-in-the-loop

Checkpoints where a human approves, edits, or rejects an agent action before
the loop continues. Captured in the packet's `humanInTheLoopPolicy`.
