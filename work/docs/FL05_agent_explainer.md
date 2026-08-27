# Agent Concepts and MCP Basics

## 1. Workflows vs. Agents
The word "agent" is currently the most abused marketing term in the AI industry. To cut through the noise, it is critical to understand the technical distinction between an automated workflow and a true AI agent.

A **workflow** is a predefined, rigid sequence of operations. In a workflow, a human architect determines the exact path the system will take. Even if a Large Language Model (LLM) is used to process data within those steps, the sequence itself is hard-coded. It operates like an assembly line: Step A must happen, followed by Step B, followed by Step C. If something unexpected occurs, the workflow breaks because it has no autonomy to diverge from the script.

An **agent**, on the other hand, is a system where the LLM acts as the routing engine itself. Instead of following a hard-coded path, the LLM is given a goal and a toolbox. It uses its reasoning capabilities to dynamically decide *which* tool to use, *when* to use it, and *how* to recover if a tool returns an error. An agent has autonomy; a workflow has rails.

**Classifying our FL-04 Pipeline:**
Our "ML Leak-Guard Reviewer" pipeline built in FL-04 is strictly a **workflow**, not an agent. It relies on a rigid prompt chain (Draft -> Critique -> Revise). Regardless of the input it receives, it blindly executes those three steps in that exact order. It cannot decide to skip a step, nor can it decide to fetch external information to improve its critique.

## 2. Understanding the Model Context Protocol (MCP)
If agents are going to have autonomy, they need a standardized way to interact with the outside world. This is where the Model Context Protocol (MCP) comes in. Often described as the "USB-C port for AI applications," MCP is an open standard that allows LLMs to securely connect to external data sources and tools without requiring developers to write custom integrations for every single service.

MCP introduces three core primitives that standardize how an AI interacts with its environment:
- **Tools:** Actionable functions the AI can execute. For example, an MCP tool might allow the AI to run a bash script, execute a SQL query against a database, or trigger a deployment pipeline. Tools give the AI hands.
- **Resources:** Readable data streams the AI can consume. An MCP resource might expose a local configuration file, a live API endpoint, or an internal knowledge base. Resources give the AI eyes.
- **Prompts:** Reusable templates and context snippets that guide the AI's behavior when interacting with specific tools or resources.

By using MCP, an agent can seamlessly discover what tools and resources are available to it at runtime, securely ask the host environment for permission to use them, and execute complex goals across completely different software ecosystems.

## 3. Upgrading FL-04 into a True Agent
Currently, our ML Leak-Guard Reviewer is a closed-loop workflow. When it critiques a proposed feature for data leakage, it is essentially just guessing based on its pre-trained knowledge of common SQL pitfalls and the text I provided. 

To upgrade this pipeline into a true **Agent**, we would need to give it autonomy and connect it to our actual data warehouse via MCP.

Here is how the agentic upgrade would work:
Instead of forcing a rigid 3-step prompt, we would give the LLM a goal: *"Evaluate this feature idea for data leakage. Do not approve it until you have mathematically proven it is safe against the historical data."*
We would then expose an MCP Server with a SQL Execution **Tool** connected to our Hugging Face dataset.

The Agent would receive the feature idea, autonomously draft a SQL query to test the temporal distribution of the columns, use the MCP Tool to execute the query against the live database, and analyze the results. If the query failed due to a schema error, the Agent would autonomously read the error log, rewrite the query, and try again without human intervention. It would only output its final critique *after* proving the logic against live data.

This shift—from a static text-generation sequence to a dynamic, tool-using, error-correcting system—is the exact boundary between a workflow and an agent.
