# Sniffington for Claude

The [Sniffington](https://sniffington.com) connector and plugin for Claude Code and Claude. Sniffington watches public posts about your brand on Reddit, X, TikTok, YouTube, Instagram, Facebook, LinkedIn, Threads, Bluesky, Hacker News and the news, reads each one with an AI check and rules out the namesakes with a note. This plugin lets Claude read that feed, check any brand and mark mentions done.

## Install in Claude Code

```
/plugin marketplace add ankurmans/sniffington-mcp
/plugin install sniffington@sniffington
```

Claude asks you to sign in with your Sniffington account the first time it uses the connector. Don't have one yet? Sign up free at https://sniffington.com/signup.

## Just the connector

Any MCP client can connect to the hosted server at `https://sniffington.com/mcp`. Setup guides for Claude, ChatGPT, Cursor, Codex, Gemini CLI and VS Code are at https://sniffington.com/agents.

## What's here

- `sniffington/`: the plugin (connector, skill, and the `/sniffington:brief` and `/sniffington:sniff` commands). Its [README](sniffington/README.md) says exactly what it sends.
- `.claude-plugin/marketplace.json`: the marketplace that lists it.

Sniffington is a hosted service from KMF Ventures LLC. This repository holds only the plugin files; the service itself is not published here. Questions: hello@sniffington.com.
