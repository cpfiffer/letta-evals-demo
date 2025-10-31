# Demo 3: Rubric Grader with Letta Agent as Judge

## Overview

This demonstrates using a Letta agent as a judge to grade responses based on a rubric:
- **Grader**: `letta_judge` - Uses a Letta agent (with LLM access) to evaluate responses
- **Rubric**: Custom evaluation criteria in `rubric.txt`
- **Extractor**: `last_assistant` - extracts the agent's response

## Why Letta Agent as Judge?

- No need for direct LLM API keys (uses Letta's LLM access)
- Can use tools during evaluation (e.g., web search, calculations)
- Perfect for nuanced evaluation criteria
- More flexible than simple string matching

## Files

- `dataset.csv`: Test cases with questions and reference answers
- `rubric.txt`: Evaluation criteria for the judge
- `suite.yaml`: Eval configuration

## Rubric Variables

The rubric can use these variables:
- `{input}`: Original question
- `{output}`: Agent's response (from extractor)
- `{ground_truth}`: Expected answer from dataset

## Running

```bash
letta-evals run suite.yaml
```

## Evaluation Flow

1. **Dataset** → Load test cases
2. **Target** → Agent responds to input
3. **Extractor** → Extract last_assistant message
4. **Grader** → Letta judge agent scores based on rubric
5. **Gate** → Require ≥0.7 average score

## Key Difference from model_judge

- `model_judge`: Direct LLM API call for grading
- `letta_judge`: Full Letta agent with tools, memory, and context
