# /docs

Here are the instructions needed to reproduce the first demo shown in this session: integrating and testing the Windows 365 for Agents MCP Server using a sample agent

**Prerequisites:** Usage of the Windows 365 for Agents playground agent. Follow the instructions provided [here](https://github.com/microsoft/windows-365-for-agents/tree/main/W365A-Playground-Agent)

## Understanding the sample agent
You can find an overview of this agent within the README.md of the sample agent. 

Overall, this is a computer use agent, built on Azure OpenAI, and powered by a GPT-5.4 model. The agent receives a user message, connects to the MCP server to get its toolkit, provisions and controls a Cloud PC session, and then enters its core loop — capture a screenshot, reason over it, take an action, and repeat until the task is complete. It's a simple agent, but it's fully integrated with Agent 365 and Windows 365 for Agents.

## Explore the components of the agent
The "ComputerUse" section is where you can dive into the components of the agent. For example,
    - "Computer Use Orchestrator" details the core screenshot → reason → action → repeat loop plus the prompt defining the agent's task. 
    - MyAgent.cs" contains the Agent 365 integration, observability tooling, and Windows 365 computer use logic.

## Wire up the MCP servers
In order for the agent to function, it needs to know which MCP server it can access. To accomplish this:
1. See what is currently available in "ToolingManifest.json"
2. See a list of MCP servers ready to go through Agent 365
    ```bash
   a365 develop list available
    ```
3. Add the Windows 365 Computer Use MCP server
   ```bash
   a365 develop add-mcp-server mcp_W365ComputerUse
    ```
4. Add the mail tools MCP server
   ```bash
   a365 develop add-mcp-server mcp_MailTools
    ```

## Testing the agent
Now you can run it locally and ensure that the MCP servers are working as intended. To accomplish this:
6. Open the **Agent 365 Playground** and connect to the local agent
7. Run a test task such as asking the agent to
   ```bash
   open Notepad and type "This is a demo of W365A"
   ```
8. Wait for **"Task completed successfully."**

### Verify
9. Review the captured screenshots (4 total). The final screenshot should show the Cloud PC with Notepad open reading **"This is a demo of Windows 365."**

