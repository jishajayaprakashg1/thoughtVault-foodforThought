### MCP : Model Context Protocol 

```
Problem statement: Say you have built an AI assistant chatbot. 
customer asks, where is my order, when will I get my refund, etc?
model has to get data from different sources like DB, 

LLM needs tools to fetch answers for different prompts
say one LLM needs yo integrate with 5 tools, then 5 custom logic needs to be written.
and if there are 3 different models connecting to 5 tools each then 3*5 = 15 custom logic needs to be written.

this is hard to build, difficult to main and breaks on swap of any model

Hence, MCP came into picture.
MCP is the connector between the llm and the tools.
Analogy of MCP: computer has different type of ports to connect hard disk, sd cards, keyboard, mouse.
USB-C port on our computer will be connected to a USB-C HUB which is in turn connected to multiple devices.
```

### Advantages
- was introduced to solve the N*M integration problem.
- it is the middle man or the connector between llm and it's tools(github, slack, DB, etc).
- it is a set of rules required for interaction between llm and tools.
- it solves the N*M integration problem.
- easy to maintain.
- more secure, as API key's need not be exposed to llm, it will be stored in mcp server.
- MCP is now(July 2026) stateless which means MCP server treats every incoming request as an independent request not as part of the same session.
  horizontal scaling, enables round robin balancing on server end.
- MCP servers : enterprise(GITHUB), open-source(community support), custom
- When we build a custom MCP server we can have an MCP server aggregator too instead of having single MCP server for each tool.

### Architecture
MCP HOST ( the AI application having the llms) -- MCP CLIENT (lives inside the host, which does the orchestration) -- MCP SERVER (translator)

1. Tools discovery : when the AI chatbot starts, MCP CLIENT will ask MCP server the tools list. Th einput schema is passed by server to client
   and now llm will have the complete tools list and it's capabilities.
2. User query: asks "Where is the order"
3. LLM decision: host decides which tool to invoke based on the user prompt
4. Host execution: host asks mcp client to tell the sever to execute the required tool,
   server will give back the response to client and then to llm
5. LLM responds:  llm which frames the user friendly response.
6. Conversation continues.

### Playwright MCP: https://playwright.dev/mcp/introduction
- Provides browser automation capabilities using Playwright.
  Enables LLMs to interact with web pages through structured accessibility snapshots — no vision models required.
- The LLM reads the accessibility snapshot, finds element refs like e5,
  and passes them as the target of the next tool call : clicking buttons, filling forms, checking checkboxes.
  No screenshots or coordinate guessing needed.
- Install an MCP client for example: vscode
- Give mcp server information client
  ```
  {
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
  }
  ```
- Give prompt to AI assitant (agent mode): github copilot. Forexampel to navigate to a particular site.
- The assistant calls MCP tools to open the browser, navigate, and interact — returning accessibility snapshots at each step:
  ```
  → browser_navigate { url: "https://demo.playwright.dev/todomvc" }

  - heading "todos" [level=1] [ref=e3]
  - textbox "What needs to be done?" [ref=e5]
   browser_type { target: "e5", text: "Buy groceries", submit: true }

  - heading "todos" [level=1] [ref=e3]
  - textbox "What needs to be done?" [ref=e5]
  - list [ref=e8]:
    - listitem [ref=e9]:
      - checkbox "Toggle Todo" [ref=e10]
      - text: Buy groceries
  - contentinfo [ref=e12]:
    - text: 1 item left
  ```
- llm will interact with the web page through the ref
- what is a snapshot: returns a structured tree of accessible elements with refs for interaction.
- If a ref is stale, the tool fails with Ref <ref> not found in the current page snapshot. Try capturing new snapshot.
- Capabilities: control which tools the MCP server exposes to the LLM.
  By default, only core tools are enabled. Add capabilities to unlock additional tool groups. enable via CLI or env or configs
  ```
  Via config:
  {
  "capabilities": ["vision", "pdf", "devtools", "network", "storage", "testing"]
  }
  ```
- 
