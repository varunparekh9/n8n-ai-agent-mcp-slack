# n8n AI Agent with MCP, Slack and Google Sheets

An AI-powered automation project built with n8n that allows users to query structured data through either n8n Chat or Slack.

The AI agent uses MCP to access a reusable Google Sheets lookup sub-workflow and dynamically retrieves only the requested record before returning a response.

## Architecture
```text
Slack / n8n Chat
        ↓
AI Agent
        ↓
MCP Client
        ↓
MCP Server
        ↓
Lookup Sub-workflow
        ↓
Google Sheets
        ↓
Dynamic Filter
        ↓
Matching Record
        ↓
AI Response
```
## Features

- Dual interface through Slack and n8n Chat
- AI agent built with n8n's LangChain agent node
- OpenAI chat model integration
- MCP client/server architecture
- Reusable n8n sub-workflows
- Dynamic Google Sheets lookup
- Natural-language tool calling
- Slack bot responses
- Dynamic channel routing
- Token optimization by filtering data before returning results to the AI agent

## Workflows

### `ai-agent-slack-chat.json`
Main orchestration workflow containing:
- n8n Chat Trigger
- Slack Trigger
- AI Agent
- OpenAI Chat Model
- MCP Client
- Conditional Slack routing
- Slack Send Message node

### `mcp-server.json`
MCP server workflow used to expose tools to the AI agent.

### `google-sheets-lookup-subworkflow.json`
Reusable lookup workflow containing:
- Sub-workflow trigger
- Google Sheets retrieval
- Dynamic filtering using `column_query` and `column_value`
- Filtered result returned to the agent

## Example

A user can ask:

`What is Sofia's phone number?`

The agent determines the appropriate lookup parameters, calls the MCP tool, retrieves only the matching Google Sheets row, and returns the requested information.

## Token Optimization

Instead of returning the entire Google Sheet to the model, the lookup sub-workflow filters the data first and returns only the matching row.

This reduced the context sent back to the AI agent and significantly lowered token usage.

## Technologies

- n8n
- OpenAI
- Model Context Protocol (MCP)
- Slack API
- Google Sheets
- LangChain-based n8n AI Agent
