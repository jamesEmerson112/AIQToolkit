# Personal Finance Workflow (Agno + AIQ Toolkit) — Technical Notes

## Overview

This project is a single, integrated workflow that combines the Agno agent framework and the AIQ toolkit to deliver a personalized financial planning agent. It is not two separate projects, but a unified example that leverages both libraries.

---

## 1. Docker Deployment

- **Build the Docker image:**
  ```bash
  docker build --build-arg AIQ_VERSION=$(python -m setuptools_scm) -t agno_personal_finance -f examples/agno_personal_finance/Dockerfile .
  ```
- **Run the Docker container:**
  ```bash
  docker run -p 8000:8000 -e NVIDIA_API_KEY -e SERP_API_KEY agno_personal_finance
  ```
- **Test the API:**
  ```bash
  curl -X 'POST' \
    'http://localhost:8000/generate' \
    -H 'accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '{"inputs": "My financial goal is to retire at age 60. I am currently 40 years old, working as a Machine Learning engineer at NVIDIA."}'
  ```

---

## 2. SerpAPI Integration

- **Purpose:**  
  SerpAPI is used for web search functionality within the workflow, enabling the agent to research financial strategies and advice.
- **Setup:**  
  - Obtain an API key from [serpapi.com](https://serpapi.com/).
  - Add `SERP_API_KEY=your_serp_api_key_here` to your `.env` file or pass it as an environment variable to Docker.
- **Usage in Workflow:**  
  The "Researcher" agent uses SerpAPI to search for relevant financial information as part of its reasoning process.

---

## 3. Prompts and Running the Workflow

- **Prompts:**  
  - System and user prompts are defined in the config YAML and in the agent descriptions/instructions in the code.
  - Example system prompt for the planner:  
    “You are a senior financial planner. Given a user's financial goals, current financial situation, and a list of research results, your goal is to generate a personalized financial plan...”
- **Run Locally:**
  ```bash
  aiq run --config_file examples/agno_personal_finance/src/aiq_agno_personal_finance/configs/config.yml --input "My financial goal is to retire at age 60. I am currently 40 years old, working as a Machine Learning engineer at NVIDIA."
  ```
- **Expected Output:**  
  A detailed, actionable financial plan tailored to the user’s input.

---

## 4. Technical Architecture

- **Main Python Files:**
  - `agno_personal_finance_function.py`: Defines the core workflow logic and agent composition.
  - `register.py`: Imports the function module to trigger registration with the AIQ toolkit.
- **Agent Composition:**
  - **Researcher Agent:**  
    - Role: Searches for financial advice, investment opportunities, and savings strategies.
    - Uses SerpAPI as a tool.
    - Generates search terms, performs web searches, and returns the most relevant results.
  - **Planner Agent:**  
    - Role: Synthesizes a personalized financial plan based on user input and research results.
    - Uses the same LLM as the researcher.
    - Focuses on clarity, coherence, and actionable advice.
- **Workflow Logic:**
  - The workflow is registered as an AIQ function using a config class and decorator.
  - The main function is asynchronous and follows a two-step process:
    1. Researcher gathers relevant information via web search.
    2. Planner generates the financial plan using the research results.
  - The function is exposed as a registered workflow, callable via config, CLI, or API.
- **Registration:**
  - `register.py` ensures the workflow is auto-registered with the AIQ toolkit when the module is imported.

---

## 5. Summary

- This is a single, unified project that demonstrates advanced agent composition (multi-agent, multi-step reasoning) using Agno and AIQ toolkit.
- It is highly configurable, supports both local and Dockerized deployment, and integrates external APIs (SerpAPI) for real-world data.
- The workflow is modular, with clear separation between research and planning agents, and can be extended with additional tools or agents as needed.
