# Exploration Checklist for examples/agents

This checklist will help you systematically review each agent architecture and its implementation in the AIQ Toolkit.

---

## Agents/ Exploration Checklist

1. **ReAct Agent (`react/`)**
   - Read the `README.md` for an overview and usage instructions.
   - Review the code and configuration files.
   - Run the example if possible and observe its behavior.
   - **Progress:**  
     - Ran: `aiq run --config_file=examples/agents/react/config.yml --input "who was Djikstra?"`
     - **Output/Observations:**
       - Multiple warnings about slow plugin/module loading (e.g., aiq_profiler_agent, aiq_agents, aiq_tools, aiq_agno, aiq_langchain, aiq_automated_description_generation, aiq_multi_frameworks).
       - **Error:** Failed to import plugin 'aiq_alert_triage_agent' due to `ModuleNotFoundError: No module named 'fcntl'` (from ansible_runner).
         - Note: `fcntl` is a Unix-only module and is not available on Windows. This may cause plugin import failures on Windows systems.
       - Other warnings about framework discovery and config overwrites.
       - Code generation tool initialized successfully.
       - **Workflow Type:** react_agent
       - **Number of Functions:** 3
       - **Number of LLMs:** 1
       - **Agent Reasoning:** Directly uses the ReAct agent to answer the question.
       - **Final Answer:**  
         "Djikstra was a Dutch computer scientist, programmer, software engineer, mathematician, and science essayist. He is best known for his work on the shortest path problem and his development of Dijkstra's algorithm, which is a widely used algorithm for finding the shortest path between nodes in a weighted graph."
       - [Add further observations or results here]

   - **Reasoning Agent (config-reasoning.yml):**
     - Ran: `aiq run --config_file=examples/agents/react/configs/config-reasoning.yml --input "who was Djikstra?"`
     - **Output/Observations:**
       - Similar plugin/module loading warnings as above.
       - The workflow type is "reasoning_agent", which augments itself with the ReAct agent as a function.
       - Uses two LLMs: nim_llm and r1_model (DeepSeek R1).
       - The agent generates a detailed reasoning plan, selects the wikipedia_search tool, and synthesizes a comprehensive answer.
       - **Workflow Type:** reasoning_agent (augmented with react_agent)
       - **Number of Functions:** 4
       - **Number of LLMs:** 2
       - **Agent Reasoning:** The reasoning_agent plans, then calls the ReAct agent as a function for tool use and answer synthesis.
       - **Final Answer:**  
         "Edsger Dijkstra was a Dutch computer scientist, programmer, software engineer, mathematician, and science essayist. He is best known for his work on algorithms, programming languages, and software engineering. Dijkstra was born in 1930 in Rotterdam, Netherlands, and studied mathematics and physics at the University of Leiden. He worked as a programmer at the Mathematical Centre in Amsterdam and later became a professor at the Technische Hogeschool Eindhoven. Dijkstra is known for his contributions to the development of structured programming languages, and he received the 1972 Turing Award for his work. He also made significant contributions to the field of distributed computing and was a pioneer in the development of the THE multiprogramming system. Dijkstra passed away in 2002, but his work continues to influence the field of computer science."
       - [Add further observations or results here]

   - **Mixture of Agents (mixture_of_agents/config.yml):**
     - **Config Structure:**
       - Two LLMs:
         - agent_orchestrator (Llama-3.1-405b-instruct): Used by the top-level ReAct agent for orchestration and reasoning.
         - agent_executor (Llama-3.3-70b-instruct): Used by sub-agents for tool execution.
       - **Sub-agents as tools:**
         - math_agent: A tool-calling agent with calculator tools (multiply, inequality, divide).
         - internet_agent: A tool-calling agent with internet tools (wikipedia_search, current_datetime).
         - code_generation: A code generation tool (Python).
       - **Workflow:**
         - The main workflow is a ReAct agent that can delegate tasks to math_agent, internet_agent, or code_generation.
         - The system prompt explicitly instructs the agent to collaborate with "experts" (the sub-agents/tools) and defines a structured format for agent reasoning and tool use.
     - **Key Features:**
       - Demonstrates agent orchestration: the top-level agent can call sub-agents as tools, enabling modular, hierarchical workflows.
       - Each sub-agent is itself a tool-calling agent, showing deep composability.
       - Uses different LLMs for orchestration and execution, allowing specialization.
       - The system prompt enforces a clear, stepwise reasoning and action format.
     - [Add further observations or results here]

   - **ReWOO Agent (rewoo/):**
     - **Overview:**
       - Demonstrates a configurable ReWOO (Reasoning WithOut Observation) agent using the AIQ toolkit.
       - The ReWOO agent plans out a sequence of reasoning steps and tool calls in advance, without waiting for intermediate observations ("plan then execute" paradigm).
       - Useful for tasks that benefit from global planning or parallel execution of actions.
     - **Setup:**
       - Requires NVIDIA API key and (optionally) a Tavily API key for internet search.
       - Install with `uv sync --all-groups --all-extras` and `uv pip install -e .`.
     - **How to Run:**
       - Example command:  
         `aiq run --config_file=examples/agents/rewoo/configs/config.yml --input "Which city held the Olympic game in the year represented by the bigger number of 1996 and 2004?"`
     - **Workflow:**
       - The agent first plans: compares 1996 and 2004, then plans to search for the city that hosted the Olympics in the larger year.
       - Executes the planned steps: uses calculator_inequality, then internet_search.
       - Synthesizes the final answer ("Athens") after executing all planned steps.
     - **Other Features:**
       - Can be run as a server (`aiq serve ...`) and supports both streaming and non-streaming HTTP requests.
       - Supports evaluation with `aiq eval ...`.
     - **Key Concept:**  
       - "Without observation" means the agent does not wait for the result of each action before planning the next; it plans the whole sequence, then executes.
     - [Add further observations or results here]

   - **Comparison: ALPHA (config.yml) vs BETA (config-reasoning.yml) vs Mixture of Agents vs ReWOO**
     - **Agent Architecture:**
       - ALPHA: Direct ReAct agent workflow.
       - BETA: Reasoning agent workflow, augmented with ReAct agent as a function.
       - Mixture: ReAct agent orchestrates multiple sub-agents (math_agent, internet_agent), each with their own tools.
       - ReWOO: ReWOO agent plans all steps before executing, then runs the plan without intermediate observations.
     - **LLMs Used:**
       - ALPHA: 1 LLM.
       - BETA: 2 LLMs.
       - Mixture: 2 LLMs (orchestrator and executor).
       - ReWOO: 1 LLM.
     - **Functions/Tools:**
       - ALPHA: 3 tools.
       - BETA: 4 functions (including react_agent as a function).
       - Mixture: Sub-agents as tools, each with their own toolset; code_generation tool.
       - ReWOO: Multiple tools (calculator_inequality, internet_search, etc.).
     - **Reasoning Process:**
       - ALPHA: Direct question answering.
       - BETA: Planning and delegation to ReAct agent.
       - Mixture: Top-level agent delegates to sub-agents for specialized tasks (math, internet search, code).
       - ReWOO: Plans all reasoning and tool calls in advance, then executes the plan.
     - **Output Quality:**
       - ALPHA: Concise.
       - BETA: Comprehensive.
       - Mixture: Highly modular, supports complex, multi-step queries.
       - ReWOO: Strategic, global planning; efficient for certain tasks.
     - **Common Issues:**
       - All encounter similar plugin warnings and fcntl error.
       - ReWOO: Requires correct API keys for all tools.

2. **Tool Calling Agent (`tool_calling/`)**
   - Read the `README.md` for details on tool-calling workflows.
   - Examine the code to see how tool invocation is implemented.
   - Try running the example and note how tools are called.

3. **Mixture of Agents (`mixture_of_agents/`)**
   - Read the `README.md` to understand agent orchestration.
   - Explore how a ReAct agent coordinates multiple tool-calling agents.
   - Run the example to see agent collaboration in action.

4. **ReWOO Agent (`rewoo/`)**
   - Read the `README.md` for the ReWOO reasoning paradigm.
   - Study the code to see how reasoning with/without observation is handled.
   - Run the example and compare its approach to the others.

5. **Shared Data (`data/`)**
   - Browse the contents to see what datasets or resources are provided.
   - Check if any examples reference or use these data files.

---

**Suggested Approach:**  
- For each agent type, start with the README, then review the code/configs, and finally try running the example if you want hands-on experience.
- Take notes on unique features, similarities, and differences between the agent architectures.
