# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview
MCP server that enables macOS automation through AppleScript, packaged as a DXT extension.

## Commands
- `npm start` - Run the MCP server locally
- `npm test` - Validate manifest.json
- `npm run build` - Build DXT package
- `npm run sign` - Self-sign the DXT package

## Architecture
- **server/index.js**: MCP server exposing single "osascript" tool
  - Executes AppleScript via Node's `execFile`
  - 30-second timeout
  - Returns output or error messages
- **manifest.json**: DXT manifest with tool metadata
- ES modules, no TypeScript
- Single dependency: `@modelcontextprotocol/sdk`
