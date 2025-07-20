# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview
This is an MCP (Model Context Protocol) server that allows AI assistants to control macOS through osascript/AppleScript commands. The project is packaged using DXT (Developer Extension Tool) for easy distribution.

## Commands

### Development
- `npm start` - Run the MCP server directly (for testing)
- `npm run build` - Build the DXT package (creates osascript-dxt.dxt)

### Installation & Usage
- The DXT package bundles the server and all dependencies

## Architecture

### Core Components
- **server/index.js**: Main MCP server implementation
  - Uses `@modelcontextprotocol/sdk` to implement the protocol
  - Exposes single tool "osascript" that executes AppleScript via Node's `execFile`
  - 30-second timeout for script execution
  - Returns script output as text or error messages

### Key Files
- **manifest.json**: DXT manifest defining the tool metadata and capabilities
- **package.json**: Node.js configuration with ES modules (`"type": "module"`)

### Technical Details
- Pure JavaScript ES modules (no TypeScript)
- Single-purpose tool focused on AppleScript execution
- Minimal dependencies - only the MCP SDK
- No test suite - simple implementation that relies on system `osascript` command

## Development Notes
- When modifying the server, test locally with `npm start` before building
- The DXT build process handles bundling all dependencies
- Error handling is implemented for script execution failures and timeouts
- The tool accepts any valid AppleScript as input
