# Demo 1: Agent File (.af)

## What is an Agent File?

An agent file (.af) is a JSON format that contains everything needed to define a Letta agent:

- **Agent Configuration**: Name, description, system prompt
- **LLM Config**: Model, temperature, context window
- **Embedding Config**: Embedding model settings
- **Tools**: Custom functions the agent can call
- **Memory Blocks**: Agent's persistent memory
- **Messages**: Initial conversation history

## Example

See `qa_agent.af` for a simple geography Q&A agent. This agent:
- Uses GPT-4o-mini
- Has a system prompt for answering geography questions
- No custom tools (just basic chat)
- No custom memory blocks

## Key Concepts to Highlight

1. Agent files are portable - can be shared and reused
2. Contains complete agent configuration
3. Used in evals with `agent_file: qa_agent.af` in suite.yaml
