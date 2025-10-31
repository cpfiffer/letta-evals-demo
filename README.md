# Letta Evals Intro Video Script

## Video Outline

### 1. Introduction (30 seconds)
- Introduce yourself
- What is Letta Evals?
  - Framework for evaluating AI agents built with Letta
  - Systematic testing for stateful AI agents
  - Test memory, tool usage, multi-turn conversations, state evolution

### 2. Core Concepts (1 minute)
Explain the evaluation flow:
**Dataset → Target (Agent) → Extractor → Grader → Gate → Result**

- **Dataset**: Test cases with inputs and expected outputs (CSV or JSONL)
- **Target**: The agent to test (specified by agent file or agent ID)
- **Extractor**: Pulls out content from agent responses (last message, memory, etc.)
- **Grader**: Scores the extracted content (tool-based or LLM-based)
- **Gate**: Pass/fail threshold for the entire evaluation
- **Result**: Metrics and pass/fail status

### 3. Agent Files (.af) (1 minute)
**Demo**: Show `1-agentfile/qa_agent.af`

- Agent files contain everything to define a Letta agent
- JSON format with:
  - Agent configuration (name, description, system prompt)
  - LLM config (model, temperature, etc.)
  - Embedding config
  - Tools (custom functions)
  - Memory blocks
  - Initial messages
- Portable and reusable
- Used in evals with `agent_file: qa_agent.af`

### 4. Simple Single-Turn Eval (2 minutes)
**Demo**: Show `2-simple/` example

- **Dataset**: `dataset.csv` with geography questions
- **Suite**: `suite.yaml` configuration
  - Target: Uses qa_agent.af
  - Extractor: `last_assistant` (gets agent's final text response)
  - Grader: `tool` with `contains` function (string matching)
  - Gate: Require 67% pass rate

**Run the eval**: `letta-evals run suite.yaml`
- Show real-time progress
- Show results summary

**Key Points**:
- Extractors: `last_assistant`, `all_assistant`, `last_turn`, `tool_output`, `memory_block`
- Tool graders: `contains`, `exact_match` (fast, deterministic)
- Gates define pass/fail criteria

### 5. Rubric Grader with Letta Agent as Judge (2 minutes)
**Demo**: Show `3-rubric/` example

- **Why rubric grading?**
  - Need nuanced evaluation
  - String matching too rigid
  - Want to grade quality, not just correctness

- **Letta Agent as Judge**:
  - Uses `letta_judge` grader type
  - No direct LLM API keys needed
  - Can use tools during evaluation
  - More flexible than simple LLMs

- **Rubric**: `rubric.txt`
  - Template with variables: `{input}`, `{output}`, `{ground_truth}`
  - Custom evaluation criteria
  - Scoring guidelines

**Run the eval**: `letta-evals run suite.yaml`

**Key Points**:
- `letta_judge` vs `model_judge`
- Rubric variables
- Scoring guidelines (0.0 to 1.0)

### 6. Multi-Turn Conversations (2 minutes)
**Demo**: Show `4-multiturn/` example

- **Why multi-turn?**
  - Test memory across conversation
  - Test state persistence
  - Real conversation patterns

- **Dataset**: `dataset.jsonl` (JSONL not CSV)
  - `input` is a list of strings
  - Each string sent sequentially

- **Memory Block Extractor**:
  - Extract from agent's memory instead of response
  - Check if agent updated memory correctly

- **Agent**: `memory_agent.af`
  - Has `user_preferences` memory block
  - Stores information across turns

**Run the eval**: `letta-evals run suite.yaml`

**Key Points**:
- Multi-turn input format
- Memory block extractor
- Testing state evolution

### 7. Wrap Up (30 seconds)
- Recap the four key areas covered
- Where to learn more:
  - GitHub: github.com/letta-ai/letta-evals
  - Docs: docs.letta.com/evals
  - Examples: examples/ directory
- Encourage viewers to try it themselves

---

## Demo Directory Structure

```
demo/
├── README.md (this file)
├── 1-agentfile/       # What is an agent file?
│   ├── qa_agent.af
│   └── README.md
├── 2-simple/          # Simple single-turn with tool grader
│   ├── dataset.csv
│   ├── suite.yaml
│   └── README.md
├── 3-rubric/          # Rubric grading with Letta agent as judge
│   ├── dataset.csv
│   ├── rubric.txt
│   ├── suite.yaml
│   └── README.md
└── 4-multiturn/       # Multi-turn with memory block extractor
    ├── dataset.jsonl
    ├── memory_agent.af
    ├── suite.yaml
    └── README.md
```

## Running the Demos

Prerequisites:
1. Letta server running: `letta server`
2. Letta Evals installed: `pip install letta-evals`

Run each demo:
```bash
cd 2-simple && letta-evals run suite.yaml
cd ../3-rubric && letta-evals run suite.yaml
cd ../4-multiturn && letta-evals run suite.yaml
```

## Tips for Video Recording

1. **Start simple**: Begin with agent files, then build up
2. **Show code**: Display the YAML and dataset files
3. **Run live**: Execute the evals and show results
4. **Explain as you go**: Walk through each component
5. **Keep it focused**: ~8-10 minutes total
