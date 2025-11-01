# Letta Evals Demo

This repository contains example code and demos for [Letta Evals](https://github.com/letta-ai/letta-evals), a testing framework for stateful AI agents. These examples accompany the [Letta Evals introduction video](https://youtube.com/@lettalabs).

## What is Letta Evals?

Letta Evals is a testing framework designed for evaluating stateful AI agents built with Letta. It enables you to:

- Test whether agents use tools correctly
- Verify agents provide accurate answers
- Check if agents remember information across conversations
- Build CI/CD pipelines for agent development
- Run benchmarks and leaderboards at scale

Letta Evals helps you build production-quality agents by providing systematic evaluation capabilities similar to continuous integration testing.

## Core Concepts

Letta Evals uses an evaluation pipeline:

**Dataset → Target → Extractor → Grader → Gate → Result**

- **Dataset**: Test cases with inputs and expected outputs (CSV or JSONL format)
- **Target**: The agent being evaluated (specified by agent file or agent ID)
- **Extractor**: Extracts specific content from agent responses (messages, memory blocks, tool calls)
- **Grader**: Scores the extracted content (tool-based or LLM-based)
- **Gate**: Pass/fail threshold that throws an error if evaluation fails
- **Result**: Metrics including average score, standard deviation, and error counts

## What's in This Repo

This repository contains four progressive examples demonstrating Letta Evals capabilities:

### Directory Structure

```
.
├── 1-agentfile/       # Introduction to agent files
│   ├── qa_agent.af
│   └── README.md
├── 2-simple/          # Simple single-turn evaluation with tool grader
│   ├── dataset.csv
│   ├── suite.yaml
│   └── README.md
├── 3-rubric/          # Rubric-based grading with Letta agent as judge
│   ├── dataset.csv
│   ├── rubric.txt
│   ├── suite.yaml
│   └── README.md
└── 4-multiturn/       # Multi-turn conversations with memory testing
    ├── dataset.jsonl
    ├── memory_agent.af
    ├── suite.yaml
    └── README.md
```

### Examples Overview

**1. Agent Files**: Learn about Letta's agent file format (.af), which stores complete agent snapshots including configuration, tools, memory blocks, and message history.

**2. Simple Evaluation**: Basic single-turn Q&A testing using tool-based grading (string matching) to verify correct answers.

**3. Rubric Grading**: Advanced evaluation using a Letta agent as judge to grade qualitative responses based on custom rubrics.

**4. Multi-Turn Testing**: Test memory persistence across multiple conversation turns, verifying agents remember information correctly.

## Prerequisites

1. **Python 3.10+** (use [uv](https://docs.astral.sh/uv/) for package management)
2. **Letta server**: Install and run Letta
   ```bash
   pip install letta
   letta server
   ```
3. **Letta Evals**: Install the evaluation framework
   ```bash
   pip install letta-evals
   ```

## Running the Examples

Each example can be run independently. Navigate to the example directory and execute:

```bash
# Simple single-turn evaluation
cd 2-simple
letta-evals run suite.yaml

# With output saved to results directory
letta-evals run suite.yaml --output results

# Rubric-based grading
cd ../3-rubric
letta-evals run suite.yaml --output results

# Multi-turn memory testing
cd ../4-multiturn
letta-evals run suite.yaml --output results
```

Each example includes a README with detailed explanations.

## Key Features Demonstrated

- **Tool-based grading**: Fast, deterministic evaluation using functions like `contains` and `exact_match`
- **Rubric grading**: Nuanced qualitative evaluation using LLMs or Letta agents as judges
- **Multi-turn conversations**: Testing state persistence and memory across conversation turns
- **Memory block extraction**: Verifying agents store and retrieve information correctly
- **Agent replication**: Creating multiple agent instances from a single agent file for parallel testing

## Learn More

- **Documentation**: [docs.letta.com/evals](https://docs.letta.com/evals)
- **Main Repository**: [github.com/letta-ai/letta-evals](https://github.com/letta-ai/letta-evals)
- **Letta Framework**: [github.com/letta-ai/letta](https://github.com/letta-ai/letta)
- **Community**: [discord.gg/letta](https://discord.gg/letta)

## Advanced Use Cases

Letta Evals supports sophisticated workflows:

- **CI/CD Integration**: Use gates to block deployments if agents regress
- **Agent Training**: Repeatedly evaluate the same agent ID to help it learn
- **Teacher-Student Patterns**: Use specialized judge agents that improve over time
- **Custom Extractors**: Write custom functions to extract any data from agent responses
- **Batch Evaluation**: Run thousands of evaluations in parallel

See the [examples directory](https://github.com/letta-ai/letta-evals/tree/main/examples) in the main Letta Evals repository for more advanced patterns.
