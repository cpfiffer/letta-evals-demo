# Demo 4: Multi-Turn Conversations

## Overview

This demonstrates evaluating multi-turn conversations with memory:
- **Multi-turn input**: List of strings instead of single string
- **Memory blocks**: Agent has persistent memory
- **Memory block extractor**: Extracts content from agent's memory
- **Grader**: Checks if memory was updated correctly

## Key Concept: Multi-Turn

In `dataset.jsonl`, the `input` field is a list:
```json
{
  "input": [
    "Remember that my favorite European capital is Paris.",
    "What's my favorite European capital?"
  ],
  "ground_truth": "Paris"
}
```

The eval framework sends each message sequentially, creating a conversation.

## Memory Block Extractor

Instead of extracting the agent's response, we extract from memory:
```yaml
extractor: memory_block
extractor_config:
  block_label: "user_preferences"
```

This checks if the agent properly stored information in its memory.

## Files

- `dataset.jsonl`: Multi-turn conversations (note: JSONL not CSV)
- `memory_agent.af`: Agent with `user_preferences` memory block
- `suite.yaml`: Eval configuration

## Running

```bash
letta-evals run suite.yaml
```

## Evaluation Flow

1. **Dataset** → Load multi-turn conversations
2. **Target** → Send each message in sequence
3. **Extractor** → Extract `user_preferences` memory block content
4. **Grader** → Check if ground_truth appears in memory
5. **Gate** → Require 100% pass rate

## Why This Matters

Multi-turn evals test:
- Memory updates across turns
- State persistence
- Context retention
- Real conversation patterns
