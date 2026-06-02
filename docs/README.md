# /docs

## Here are the step-by-step instructions needed to repro the first demo shown in this session: integrating and testing the Windows 365 for Agents MCP Server

**Prerequisites:** Usage of the Windows 365 for Agents playground agent. Follow the instructions instructions provided [here] (https://github.com/microsoft/windows-365-for-agents/tree/main/W365A-Playground-Agent)

### Understand the agent structure
1. **Computer Use Orchestrator** — holds the core `screenshot → reason → action → repeat` loop plus the prompt defining the agent's task.
2. **`MyAgent.cs`** — contains the Agent 365 integration, observability tooling, and Windows 365 computer use logic. At runtime the agent discovers which MCP servers it can access and uses MCP metadata to know how/when to call them.
3. **Tooling manifest** — declares which MCP servers the agent can access. Starts empty (no servers = no Windows 365 access).

### Wire up the MCP servers
4. List the MCP servers available in the tenant:
   ```bash
   a365 list available
   ```
5. Add the Windows 365 Computer Use MCP server (pulls it into the manifest and writes the auth/config the agent needs):
   ```bash
   a365 add mcp server
   ```
6. Add the Mail (Outlook) tools MCP server the same way:
   ```bash
   a365 add mcp server
   ```
7. Confirm the manifest is updated — the agent now has access to every tool in those MCP servers.

### Run and test locally
8. Kick off a local build to spin the agent up as a local server.
9. Open the **Agent 365 Playground** and connect to the local agent (you'll see live logs on the right for tracing each tool call).
10. Run a test task: ask the agent to **open Notepad and type a phrase**.
    - The agent acquires a Windows 365 Cloud PC session (checks accessible pools and available machines to check out).
    - First-time spin-up takes a few moments.
    - A screenshot is captured on every step.

### Verify
11. Wait for **"Task completed successfully."**
12. Review the captured screenshots (4 total). The final screenshot should show the Cloud PC with Notepad open reading **"This is a demo of Windows 365."**

---

A couple of notes for your GitHub doc:
- The exact CLI syntax for the add command (server name/flags) wasn't spoken in the narration — it just says "add mcp server." You may want to fill in the precise argument (e.g., the server identifier) before publishing.
- Want me to also save this as a `.md` file in your workspace, or are you set with the inline version?
This folder is for documentation and step-by-step content for your session.

## What goes here

- **Labs/Workshops**: Step-by-step instructions organized into numbered exercises (e.g., `01-setup/`, `02-first-exercise/`)
- **Demos**: Walkthrough documentation explaining the demo code in `/src`
- **Breakouts**: Supplementary documentation, diagrams, or reference material

## Tips

- Use numbered prefixes for ordering: `01-setup/`, `02-exercise/`, `03-wrap-up/`
- Each subfolder can have its own `README.md` or `index.md`
- Keep images in an `assets/` subfolder if needed
- If your session doesn't have documentation beyond the README, feel free to remove this folder
