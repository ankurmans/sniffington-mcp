# Sniffington for Claude Code

Sniffington watches public posts about your brand on Reddit, X, TikTok, YouTube, Instagram, Facebook, LinkedIn, Threads, Bluesky, Hacker News and the news. An AI reads each post, keeps the ones that are really about you and rules out the namesakes with a note. This plugin lets Claude read that feed for you.

## What it adds

- The Sniffington connector (a remote MCP server at `https://sniffington.com/mcp`), signed in with your Sniffington account over OAuth.
- A skill that tells Claude which tool to call for what you ask.
- `/sniffington:brief` for what needs you today, and `/sniffington:sniff <brand>` to check any brand, a competitor included.

## Set up

```
/plugin marketplace add ankurmans/sniffington-mcp
/plugin install sniffington@sniffington
```

Claude asks you to sign in when it first uses the connector. Choose read only, or read and write if you want Claude to mark mentions done or add keywords. Don't have an account? The free plan covers one brand on ten platforms (Facebook comes with the paid plans), and you can sign up at https://sniffington.com/signup.

## What it sends

Everything goes to `sniffington.com` over HTTPS and nowhere else. When Claude calls a tool, the arguments it chooses (a brand name, a filter, a mention id) are sent to your Sniffington workspace, and the results come back into the conversation. The plugin runs no scripts, installs no packages and bundles no server. It never posts to a social network; replies are yours to write.

## Privacy and support

Privacy policy: https://sniffington.com/privacy. Questions and problems: hello@sniffington.com. More setup guides, including other AI clients, are at https://sniffington.com/agents.
