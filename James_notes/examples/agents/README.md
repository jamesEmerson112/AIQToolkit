# Exploration Checklist for examples/agents

This checklist will help you systematically review each agent architecture and its implementation in the AIQ Toolkit.

---

## Agents/ Exploration Checklist

1. **ReAct Agent (`react/`)**
   ... (content unchanged for brevity) ...

   - **ReWOO Agent (rewoo/):**
     ... (content unchanged for brevity) ...

   - **Agno Personal Finance (agno_personal_finance/):**
     - **Overview:**
       - A personal financial planner workflow built on Agno and the AIQ toolkit.
       - Generates personalized financial plans using NVIDIA NIM (or OpenAI) models.
       - Automates research, planning, and creation of tailored budgets, investment strategies, and savings goals.
       - Revised from the Awesome-LLM-App's AI Personal Finance Planner.
     - **Key Features:**
       - Uses AIQ toolkit's ReAct agent and plugin system.
       - Configurable via YAML; supports custom tools and high-level APIs.
       - Integrates with Agno for multimodal, multi-agent capabilities.
     - **Setup:**
       - Install with: `uv pip install -e examples/agno_personal_finance`
       - Requires NVIDIA_API_KEY and SERP_API_KEY (for search functionality).
       - Add both keys to your .env file.
     - **How to Run:**
       - Example command:  
         `aiq run --config_file examples/agno_personal_finance/src/aiq_agno_personal_finance/configs/config.yml --input "My financial goal is to retire at age 60. I am currently 40 years old, working as a Machine Learning engineer at NVIDIA."`
     - **Deployment:**
       - Can be built and run as a Docker container for API deployment.
       - Example:  
         `docker build ...` and `docker run ...` (see README for details)
     - **Expected Output:**
       - Produces a detailed, personalized financial plan with actionable steps and investment strategies.
     - [Add further observations or results here]

   - **Comparison: ALPHA (config.yml) vs BETA (config-reasoning.yml) vs Mixture of Agents vs ReWOO vs Agno Personal Finance**
     - **Agent Architecture:**
       - ALPHA: Direct ReAct agent workflow.
       - BETA: Reasoning agent workflow, augmented with ReAct agent as a function.
       - Mixture: ReAct agent orchestrates multiple sub-agents (math_agent, internet_agent), each with their own tools.
       - ReWOO: ReWOO agent plans all steps before executing, then runs the plan without intermediate observations.
       - Agno Personal Finance: ReAct agent for financial planning, leverages Agno and external search tools.
     - **LLMs Used:**
       - ALPHA: 1 LLM.
       - BETA: 2 LLMs.
       - Mixture: 2 LLMs (orchestrator and executor).
       - ReWOO: 1 LLM.
       - Agno Personal Finance: 1 LLM (NIM or OpenAI).
     - **Functions/Tools:**
       - ALPHA: 3 tools.
       - BETA: 4 functions (including react_agent as a function).
       - Mixture: Sub-agents as tools, each with their own toolset; code_generation tool.
       - ReWOO: Multiple tools (calculator_inequality, internet_search, etc.).
       - Agno Personal Finance: Financial research, planning, and search tools (SERP API).
     - **Reasoning Process:**
       - ALPHA: Direct question answering.
       - BETA: Planning and delegation to ReAct agent.
       - Mixture: Top-level agent delegates to sub-agents for specialized tasks (math, internet search, code).
       - ReWOO: Plans all reasoning and tool calls in advance, then executes the plan.
       - Agno Personal Finance: Researches, plans, and synthesizes a financial plan using external search and reasoning.
     - **Output Quality:**
       - ALPHA: Concise.
       - BETA: Comprehensive.
       - Mixture: Highly modular, supports complex, multi-step queries.
       - ReWOO: Strategic, global planning; efficient for certain tasks.
       - Agno Personal Finance: Actionable, personalized financial advice.
     - **Common Issues:**
       - All encounter similar plugin warnings and fcntl error.
       - ReWOO: Requires correct API keys for all tools.
       - Agno Personal Finance: Requires SERP_API_KEY for search.

2. **Tool Calling Agent (`tool_calling/`)**
   ... (content unchanged for brevity) ...

3. **Mixture of Agents (`mixture_of_agents/`)**
   ... (content unchanged for brevity) ...

4. **ReWOO Agent (`rewoo/`)**
   ... (content unchanged for brevity) ...

5. **Shared Data (`data/`)**
   ... (content unchanged for brevity) ...

---

**Suggested Approach:**  
- For each agent type, start with the README, then review the code/configs, and finally try running the example if you want hands-on experience.
- Take notes on unique features, similarities, and differences between the agent architectures.
