# LangChain Notes for AI App Development

# What is LangChain?

LangChain is a framework that helps developers build AI applications using LLMs like:

- Gemini
- OpenAI
- Groq
- Claude

It helps connect:

- Models
- Agents
- Tools
- Memory
- Structured Output
- Streaming
- RAG systems

Official Website:
https://www.langchain.com/

---

# Installing LangChain

## Install Core Packages

```bash
npm install @langchain/core
```

## Gemini

```bash
npm install @langchain/google-genai
```

## OpenAI

```bash
npm install @langchain/openai
```

## Groq

```bash
npm install @langchain/groq
```

---

# Environment Variables

Create:

```txt
.env.local
```

Example:

```env
GOOGLE_API_KEY=your_key
OPENAI_API_KEY=your_key
GROQ_API_KEY=your_key
```

---

# Using Gemini Model

```ts
import { ChatGoogleGenerativeAI } from "@langchain/google-genai";

const model = new ChatGoogleGenerativeAI({
  model: "gemini-2.0-flash",
  apiKey: process.env.GOOGLE_API_KEY,
});
```

---

# Using OpenAI Model

```ts
import { ChatOpenAI } from "@langchain/openai";

const model = new ChatOpenAI({
  model: "gpt-4o-mini",
  apiKey: process.env.OPENAI_API_KEY,
});
```

---

# Using Groq Model

```ts
import { ChatGroq } from "@langchain/groq";

const model = new ChatGroq({
  model: "llama3-8b-8192",
  apiKey: process.env.GROQ_API_KEY,
});
```

---

# Invoking Model

```ts
const response = await model.invoke("Hello");
console.log(response.content);
```

---

# Streaming Output (Chunk Output)

Streaming means getting output word-by-word or chunk-by-chunk like ChatGPT.

```ts
const stream = await model.stream("Explain binary search");

for await (const chunk of stream) {
  console.log(chunk.content);
}
```

Benefits:
- Fast UI updates
- Better user experience
- Realtime chat apps

---

# Message Types in LangChain

## HumanMessage

Represents user input.

```ts
new HumanMessage("Explain OS scheduling")
```

---

## AIMessage

Represents AI response.

```ts
new AIMessage("OS scheduling decides...")
```

---

## SystemMessage

Controls AI behavior.

```ts
new SystemMessage("You are a coding teacher")
```

---

# Example

```ts
import {
  HumanMessage,
  SystemMessage,
} from "@langchain/core/messages";

const response = await model.invoke([
  new SystemMessage("You are a coding tutor"),
  new HumanMessage("Explain linked list"),
]);
```

---

# What are Agents?

Agents are AI systems that can:

- Think
- Choose tools
- Make decisions
- Perform tasks automatically

Normal LLM:
Input → Output

Agent:
Input → Think → Use Tool → Output

---

# Creating Tools

Tools give abilities to agents.

Example:
- Calculator
- Weather checker
- Database search
- Code analyzer

---

# Example Tool

```ts
import { tool } from "@langchain/core/tools";

const calculatorTool = tool(
  async ({ a, b }) => {
    return a + b;
  },
  {
    name: "calculator",
    description: "Adds two numbers",
  }
);
```

---

# Creating Agent

```ts
import { createReactAgent } from "@langchain/langgraph/prebuilt";
```

---

# Creating Agent with Tools

```ts
const agent = createReactAgent({
  llm: model,
  tools: [calculatorTool],
});
```

---

# Calling Agent

```ts
const response = await agent.invoke({
  messages: [
    {
      role: "user",
      content: "What is 5 + 10?",
    },
  ],
});

console.log(response);
```

---

# Structured Output

Structured output forces AI to return data in proper format.

Without structured output:
- messy text
- inconsistent output

With structured output:
- JSON
- reliable data
- easy frontend integration

---

# Install Zod

```bash
npm install zod
```

---

# Example Structured Output

```ts
import { z } from "zod";

const schema = z.object({
  title: z.string(),
  summary: z.string(),
});
```

---

# Using Structured Output

```ts
const structuredModel = model.withStructuredOutput(schema);

const response = await structuredModel.invoke(
  "Generate project summary"
);

console.log(response);
```

---

# Short-Term Memory

Memory helps AI remember conversation.

Example:
- previous questions
- chat history
- user context

---

# Memory Example

```ts
const messages = [
  new HumanMessage("My name is Gurkirat"),
  new HumanMessage("What is my name?"),
];
```

AI remembers previous messages.

---

# Middleware

Middleware runs between request and response.

Used for:
- Logging
- Security
- Rate limiting
- Analytics
- Token tracking

---

# Example Middleware Use Cases

## Logging

```ts
console.log("Request received");
```

## Error Handling

```ts
try {
  // code
} catch (error) {
  console.log(error);
}
```

---

# Recommended Learning Order

## Step 1

Learn:
- Basic model calling

---

## Step 2

Learn:
- Streaming output

---

## Step 3

Learn:
- Messages
- HumanMessage
- AIMessage
- SystemMessage

---

## Step 4

Learn:
- Tools

---

## Step 5

Learn:
- Agents

---

## Step 6

Learn:
- Structured output

---

## Step 7

Learn:
- Memory

---

## Step 8

Learn:
- Middleware

---

# Best Project Idea

# AI Coding Tutor

Features:
- Explain code
- Fix bugs
- Generate MCQs
- Generate assignments
- Streaming chat
- Remember conversations
- Use coding tools
- AI agents

---

# Recommended Tech Stack

Frontend:
- Next.js
- Tailwind CSS

Backend:
- LangChain

Models:
- Gemini
- Groq
- OpenAI

Database:
- Supabase

Deployment:
- Vercel

---

# Suggested Project Flow

User → Agent → Tools → AI Response

Example:

User asks:
"Fix my code"

Agent decides:
- Use bug fixing tool

Tool analyzes code

AI returns:
- Fixed code
- Explanation

---

# Deployment

## Deploy Frontend

Use:
https://vercel.com/

---

# Deploy Database

Use:
https://supabase.com/

---

# Important LangChain Concepts

| Concept | Meaning |
|---|---|
| Model | AI model like Gemini |
| Streaming | Output in chunks |
| Message | Conversation format |
| Tool | Extra ability for AI |
| Agent | AI that uses tools |
| Memory | AI remembers chat |
| Structured Output | Proper JSON response |
| Middleware | Runs between request and response |

---

# Final Advice

Do not directly jump into advanced agents.

Build step-by-step:

1. Basic Chat App
2. Streaming
3. Messages
4. Tools
5. Agents
6. Structured Output
7. Memory
8. Middleware
9. RAG
10. Multi-Agent Systems

This is the best way to properly learn AI engineering.
