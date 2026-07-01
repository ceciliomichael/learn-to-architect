# Option 06: Autonomous Agent Tool-Calling Orchestrator

**Difficulty:** Expert
**Primary Concepts:** Discriminated unions, advanced generics, async/await, error resilience, state machines, recursion

---

## Why Pure TypeScript Matters for AI

Before you can build production-grade AI agents with real LLMs (OpenAI, Anthropic, Gemini), you must master the underlying engine. Real LLMs don't execute tools  -  they return text asking *your TypeScript engine* to execute tools. If your tool-calling loop lacks strict types, error boundaries, or state management, your agent will hallucinate, crash, or enter infinite loops.

In this project, you will build a **pure TypeScript Agent Engine** with a simulated LLM brain.

---

## Domain

An **AgentTool** defines a capability the agent can use:

```typescript
interface AgentTool<TInput = any, TOutput = any> {
  name: string;
  description: string;
  validateInput(raw: unknown): raw is TInput; // Custom type guard!
  execute(input: TInput): Promise<TOutput>;
}
```

A **Message** represents the conversation state:

```typescript
type UserMessage = { role: "user"; content: string };
type AssistantMessage = { role: "assistant"; content: string };
type ToolCallMessage = {
  role: "tool_call";
  toolName: string;
  toolCallId: string;
  arguments: unknown;
};
type ToolResultMessage = {
  role: "tool_result";
  toolCallId: string;
  toolName: string;
  result: unknown;
  error?: string;
};

type AgentMessage = UserMessage | AssistantMessage | ToolCallMessage | ToolResultMessage;
```

---

## Core Requirements

Build an `AgentOrchestrator` class:

```typescript
registerTool<TIn, TOut>(tool: AgentTool<TIn, TOut>): void
// Registers a tool. Throws if tool name is duplicate.

runTurn(prompt: string, options?: { maxSteps?: number }): Promise<AgentMessage[]>
// Executes the autonomous loop until the agent produces a final text answer
// or exceeds maxSteps (default: 5).
```

### The Simulated Brain (Mock LLM)

Since we aren't calling external web APIs, create a `MockLLMBrain` class that decides what to do based on input keywords or regex patterns:
1. If the user asks `"What is the weather in Tokyo?"`, the mock brain returns a `ToolCallMessage` calling `get_weather` with `{ location: "Tokyo" }`.
2. When the orchestrator executes the tool and appends the `ToolResultMessage`, the brain sees the result and returns an `AssistantMessage`: `"The weather in Tokyo is 22°C and sunny."`
3. If the user asks a multi-step question (`"Find the stock price of AAPL and convert 150 USD to EUR"`), the agent must execute step 1, feed result back, execute step 2, feed result back, and answer.

---

## Resilience & Error Recovery Rules

Real tools fail. Your orchestrator must never crash:
- If a tool's `validateInput` returns `false`, append a `ToolResultMessage` with error `"INVALID_INPUT: parameters did not match expected schema"` and let the agent retry.
- If `tool.execute()` throws an exception, catch it and append `error: "TOOL_EXECUTION_FAILED: <error.message>"`.
- If the loop hits `maxSteps`, return an `AssistantMessage` explaining: `"Agent stopped: Maximum reasoning steps exceeded."`

---

## What Your Final index.ts Should Demonstrate

1. Register at least 3 tools: `search_database`, `calculate_math`, and `fetch_user_record`.
2. Run a simple prompt that requires 1 tool call.
3. Run a complex prompt requiring 2 sequential tool calls.
4. Run a prompt with deliberately bad parameters to demonstrate the agent receiving an error message and self-correcting.
