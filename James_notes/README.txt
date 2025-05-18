===============================================================================
NVIDIA AGENT INTELLIGENCE TOOLKIT (AIQ TOOLKIT)
===============================================================================

Copyright (c) 2024-2025, NVIDIA CORPORATION & AFFILIATES.
Licensed under the Apache License, Version 2.0.

-------------------------------------------------------------------------------
ASCII BANNER
-------------------------------------------------------------------------------
 _   _ _____ _____     _        _    _     _ _    _ _    _ _ _    _ 
/ \ | |_   _|_   _|   / \      / \  | |  | | |  | | |  | | | |  | |
/ _ \| | | |   | |    / _ \    / _ \ | |  | | |  | | |  | | | |  | |
/ ___ \ | | |   | |   / ___ \  / ___ \| |__| | |__| | |__| | | |__| |
/_/   \_\ |_|   |_|  /_/   \_\/_/   \_\_____/ \____/ \____/|_|\____/ 

-------------------------------------------------------------------------------

INTRODUCTION

The NVIDIA Agent Intelligence Toolkit (AIQ toolkit) is a comprehensive software library designed to streamline the integration, management, and deployment of intelligent software agents.

Intelligent agents are autonomous software entities capable of performing tasks, making decisions, and interacting with various data sources and tools without constant human intervention.

AIQ toolkit provides a unified, flexible, and lightweight framework that allows developers to easily connect existing enterprise agents to diverse data sources and tools, irrespective of the underlying technology or framework.

This toolkit is particularly beneficial for developers and researchers in artificial intelligence, machine learning, and software engineering who are looking to build robust, scalable, and maintainable agent-based systems.

**NOTE:**  
Previously known as AgentIQ, the toolkit has been renamed to AIQ toolkit. The API remains unchanged and fully compatible with previous versions.  
- Users should update their dependencies to reference `aiqtoolkit` instead of `agentiq`.  
- The older `agentiq` package is temporarily available for backward compatibility but will eventually be phased out.

-------------------------------------------------------------------------------
KEY FEATURES
-------------------------------------------------------------------------------

1. **Framework Agnostic**
   - Integrates seamlessly with various agent frameworks (LangChain, LlamaIndex, CrewAI, Microsoft Semantic Kernel, custom Python-based agents).
   - Leverage your existing technology stack without rewriting or migrating current solutions.

   *Example Scenario:*  
   Enhance a LangChain-based chatbot by integrating new data sources or tools without rewriting the chatbot.

   *ASCII Visualization:*  
   [Customer Query] → [LangChain Chatbot] → [AIQ toolkit Integration Layer] → [External Data Sources]

2. **Reusability**
   - Emphasizes modularity and reusability.
   - Components (agents, tools, workflows) are designed as reusable modules.
   - Build once, reuse across multiple projects.

   *Example Scenario:*  
   Develop a "Wikipedia Search" tool and reuse it across multiple agents and workflows.

   *ASCII Visualization:*
   +-------------------+      +-------------------+      +-------------------+
   | Wikipedia Search  |<---->| Agent A (Research)|      | Agent B (Summary) |
   +-------------------+      +-------------------+      +-------------------+
            ^                        ^                          ^
            |                        |                          |
            +------------------------+--------------------------+

3. **Rapid Development**
   - Provides pre-built agents, tools, and workflows for quick adaptation and customization.
   - Accelerates prototyping and iterative improvements.

   *Example Scenario:*  
   Prototype a news summarizer agent using a pre-built "React Agent" workflow.

   *ASCII Visualization:*  
   [Pre-built React Agent] → [Customize Summarization Logic] → [News Summarizer Agent]

4. **Profiling**
   - Includes profiling capabilities to analyze agent workflow performance.
   - Identify bottlenecks, measure execution times, and track resource usage.

   *Example Scenario:*  
   Profile a complex workflow to pinpoint slow components.

   *ASCII Visualization:*  
   [Start] → [Agent A: 120ms] → [Tool X: 50ms] → [Agent B: 200ms] → [End]

5. **Observability**
   - Integrates with OpenTelemetry-compatible tools (Phoenix, W&B Weave).
   - Enables real-time monitoring, debugging, and analysis.

   *Example Scenario:*  
   Monitor production agent workflows in real-time with observability tools.

   *ASCII Visualization:*  
   [Agent Workflow] → [Observability Tool (Phoenix)] → [Real-time Monitoring Dashboard]

6. **Evaluation System**
   - Built-in tools for systematic testing and improvement of agent accuracy and reliability.
   - Enables continuous validation and improvement.

   *Example Scenario:*  
   Automatically compare agent classifications against known correct results.

   *ASCII Visualization:*  
   [Agent Classification Output] → [Evaluation Tool] → [Accuracy Score: 95%]

7. **User Interface**
   - Provides a user-friendly chat-based interface for interacting with agents.
   - Directly query agents, visualize responses, and debug workflows interactively.

   *Example Scenario:*  
   Test an agent that retrieves animal information using the chat-based UI.

   *ASCII Visualization:*  
   User: "List aardvark subspecies"  
   Agent: "1. Orycteropus afer afer..."

8. **Full MCP Support**
   - Fully supports the Model Context Protocol (MCP) for standardized communication between AI models and external tools.
   - Can act as both MCP client and server.

   *Example Scenario:*  
   Seamlessly consume tools from an external MCP server.

   *ASCII Visualization:*  
   [External MCP Server] ← MCP Protocol → [AIQ toolkit Agent] ← MCP Protocol → [External Client]

-------------------------------------------------------------------------------
COMPONENT OVERVIEW
-------------------------------------------------------------------------------

**High-level architecture of AIQ toolkit:**

+-------------------+      +-------------------+      +-------------------+
|    User Interface |<---->|     Workflows     |<---->|      Agents       |
+-------------------+      +-------------------+      +-------------------+
         |                        |                          |
         v                        v                          v
+-------------------+      +-------------------+      +-------------------+
|      Plugins      |      |      Tools        |      |   Data Sources    |
+-------------------+      +-------------------+      +-------------------+

-------------------------------------------------------------------------------
GETTING STARTED
-------------------------------------------------------------------------------

(Installation and Hello World example steps remain the same as previously detailed, providing clear, step-by-step instructions.)

-------------------------------------------------------------------------------
EXTENDED HELLO WORLD EXAMPLE
-------------------------------------------------------------------------------

**Detailed Workflow Execution Example:**

User Input: "List five subspecies of Aardvarks"  
   |  
   v  
[AIQ toolkit Workflow]  
   |  
   v  
[Wikipedia Search Tool] → Retrieves relevant Wikipedia articles  
   |  
   v  
[Agent Reasoning] → Processes retrieved information  
   |  
   v  
[Agent Response] → Generates structured response  
   |  
   v  
Console Output:  
"1. Orycteropus afer afer (Southern aardvark)  
 2. O. a. adametzi (Western aardvark)  
 3. O. a. aethiopicus  
 4. O. a. angolensis  
 5. O. a. erikssoni"

-------------------------------------------------------------------------------
FEEDBACK AND SUPPORT
-------------------------------------------------------------------------------

Your feedback is valuable!  
Report issues or request features via GitHub:  
https://github.com/NVIDIA/AIQToolkit/issues

-------------------------------------------------------------------------------
ACKNOWLEDGEMENTS
-------------------------------------------------------------------------------

AIQ toolkit leverages several open-source projects, including:
- CrewAI
- FastAPI
- LangChain
- Llama-Index
- Mem0ai
- Ragas
- Semantic Kernel
- uv

===============================================================================
