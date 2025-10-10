# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview
MCP server that enables macOS automation through AppleScript, packaged as an MCP Bundle (`.mcpb` file).

## Commands
- `npm start` - Run the MCP server locally via stdio
- `npm test` - Validate manifest.json using mcpb
- `npm run build` - Build and clean the `.mcpb` package
- `npm run sign` - Self-sign the `.mcpb` package
- `npm ci` - Clean install dependencies (used in CI)

## Development Workflow
- CI/CD pipeline runs on push/PR to main branch
- Automated releases: creates GitHub release with built `.mcpb` on every push to main
- Requires `@anthropic-ai/mcpb` CLI tool for packaging operations

## Architecture
- **server/index.js**: MCP server implementing Model Context Protocol
  - Exposes single "osascript" tool via MCP protocol
  - Implements `ListToolsRequest` and `CallToolRequest` handlers
  - Executes AppleScript via Node's `execFile` with 30-second timeout
  - 1MB maxBuffer limit for osascript output
  - Communicates via stdio transport (StdioServerTransport)
  - Returns output or error messages in MCP-compliant format
- **manifest.json**: MCP Bundle manifest with tool metadata and server configuration
- ES modules (type: "module"), no TypeScript
- Single runtime dependency: `@modelcontextprotocol/sdk`
