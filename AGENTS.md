# AGENTS.md - Gmail MCP Server (Fork)

## Project Overview
This repository is a fork of `GongRzhe/Gmail-MCP-Server`, providing a Model Context Protocol (MCP) server for Gmail.
It allows AI assistants (Claude, Gemini, etc.) to interact with Gmail (read, send, search, label).

## Development Setup

1.  **Install Dependencies:**
    ```bash
    npm install
    ```

2.  **Build:**
    ```bash
    npm run build
    ```
    This compiles TypeScript from `src/` to `dist/`.

3.  **Authentication:**
    - Place `gcp-oauth.keys.json` in the working directory (or global config path).
    - Run the auth flow:
      ```bash
      npm run auth
      ```
    - Follow the browser instructions to generate `credentials.json` / tokens.

4.  **Running:**
    - **Stdio Mode (Default):**
      ```bash
      npm start
      ```
    - **HTTP/SSE Mode (via Supergateway):**
      ```bash
      npx supergateway --stdio "npm start" --port 3001
      ```

## Key Files & Structure
- `src/index.ts`: Main entry point. Defines tools and handles MCP requests.
- `package.json`: Defines scripts and dependencies.

## Planned Improvements
- **Search Preview:** Modify the `search_messages` (or `list_messages`) tool to fetch full message details (snippet, body) for each result instead of just returning IDs. This avoids the N+1 round-trip problem for the LLM.
- **Progressive Disclosure:** Implement "smart" tools that analyze threads or contexts before presenting raw data.

## Note for Agents
When modifying `src/index.ts`, remember to run `npm run build` before testing changes.
