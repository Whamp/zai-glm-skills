# zai-mcp-servers Skill

This is a Claude Code skill designed to help agents use ZAI MCP servers more successfully on their first attempt.

## Purpose

When working with MCP servers from ZAI, agents may not always know the optimal way to interact with them or which tool to use for specific tasks. This skill provides guidance to agents on:

- Selecting the appropriate MCP server tool for the task at hand
- Understanding how to format prompts effectively
- Avoiding common pitfalls when using image/video analysis capabilities

## MCP Servers Covered

This skill covers the following ZAI MCP server tools:

- **ui_to_artifact** - Convert UI screenshots to code, prompts, specs, or descriptions
- **extract_text_from_screenshot** - OCR for extracting text from images
- **diagnose_error_screenshot** - Analyze error messages and stack traces
- **understand_technical_diagram** - Interpret architecture diagrams, flowcharts, UML, etc.
- **analyze_data_visualization** - Extract insights from charts and graphs
- **ui_diff_check** - Compare two UI screenshots for differences
- **analyze_image** - General-purpose image analysis
- **analyze_video** - Video content analysis

## Installation

Place this skill file in your Claude Code skills directory to enable agents to use it automatically when relevant tasks arise.
