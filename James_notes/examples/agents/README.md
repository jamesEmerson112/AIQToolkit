# Exploration Checklist for examples/agents

This checklist will help you systematically review each agent architecture and its implementation in the AIQ Toolkit.

---

## Agents/ Exploration Checklist

1. **ReAct Agent (`react/`)**
   - Read the `README.md` for an overview and usage instructions.
   - Review the code and configuration files.
   - Run the example if possible and observe its behavior.

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
