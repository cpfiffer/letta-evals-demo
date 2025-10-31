# Demo 2: Simple Single-Turn Eval

## Overview

This demonstrates a basic single-turn evaluation using:
- **Extractor**: `last_assistant` - extracts the agent's final response
- **Grader**: `tool` grader with `contains` function - checks if ground_truth appears in response
- **Gate**: Pass if 67% (2/3) of test cases pass

## Files

- `dataset.csv`: Test cases with input questions and ground_truth answers
- `suite.yaml`: Evaluation configuration
- Uses agent from `../1-agentfile/qa_agent.af`

## Running

```bash
letta-evals run suite.yaml
```

## Evaluation Flow

1. **Dataset** → Load test cases from dataset.csv
2. **Target** → Send each input to the agent
3. **Extractor** → Extract last_assistant message
4. **Grader** → Check if ground_truth is contained in extracted text
5. **Gate** → Require ≥67% pass rate

## Key Concepts

- **last_assistant extractor**: Gets the agent's final text response
- **contains grader**: Simple string matching (case-insensitive)
- **Gate**: Pass/fail threshold for the entire eval
