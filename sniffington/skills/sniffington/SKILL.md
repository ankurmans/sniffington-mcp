---
name: sniffington
description: Check what people said about a brand on Reddit, X, TikTok, YouTube, Instagram, Facebook, LinkedIn, Threads, Bluesky, Hacker News and the news, using the Sniffington MCP server. Use when the user asks what needs their attention today, wants to read or triage brand mentions, asks about sentiment trends, or wants a quick check of any brand (their own, a competitor or a name they're considering).
---

# Sniffington

Sniffington watches public posts about a brand, reads each one with an AI check, keeps the ones that are really about the brand and rules out namesakes with a short note. It never posts anything anywhere. Replies are for the human to write.

## Connect it

The skill only works when the Sniffington MCP server is connected.

```bash
claude mcp add --transport http sniffington https://sniffington.com/mcp
```

Sign in with OAuth when prompted and pick read only or read and write. If your client can't sign in, create an API key in the app under Integrations and pass it as a Bearer token. Setup pages for other clients are at https://sniffington.com/agents.

## No account yet?

Ask for one in the person's name. They stay the owner and approve it by email.

```bash
curl -X POST https://sniffington.com/api/agent/signup -H "content-type: application/json" \
  -d '{"email":"person@example.com","agent_name":"Claude"}'
```

Tell the person to open the email we send and approve. Then poll the `poll_url` from the reply with `Authorization: Bearer <poll_secret>` until it returns `api_key` (shown once, so store it). A 202 means keep waiting, a 403 means they declined. The key has a daily budget for costly actions; `whoami` shows what is left, and a 429 with `key_budget` means stop and tell the person.

To upgrade, call `request_upgrade` and give the person the link. Nothing is charged until they pay.

## Which tool, when

| The user asks | Call |
|---|---|
| "What needs me today?", "anything I should reply to?" | `get_brief` first. It returns open mentions, most urgent first, each with the AI's one-line reason. |
| "Show me the negative posts about X this week" | `list_mentions` with `project`, `sentiment`, `status`, `urgency`, `q` or `range`. Page through results if there are more. |
| "How did sentiment move this month?" | `get_analytics`. |
| "Mark these as done" / "flag this for follow-up" | `update_mention` with `done` or `follow_up`. Needs a read and write connection. |
| "What are people saying about <brand>?" for a brand the workspace doesn't track | `sniff_brand`. Pass `about` (one line on what the brand is) when the name is common, so namesakes are ruled out. |
| "Which workspace is this?" or a write fails | `whoami`. It shows the workspace, its plan, and whether the connection can make changes. |
| ChatGPT-style search and open | `search` finds mentions, `fetch` opens one by id. |

## How to answer

- Lead with the answer. For a brief, give the count and the top few posts with author, platform, the reason and the link.
- Quote the AI's reason as given. Don't invent urgency or sentiment the tool didn't return.
- Ruled-out posts are namesakes. Don't surface them unless the user asks why a post is missing, then show the note on it.
- `sniff_brand` is capped at 10 a day per workspace. Say so if it refuses; don't loop.
- Never offer to post or reply through Sniffington. If the user wants a draft reply, write it yourself from the fetched post and hand it back to them.

## Example prompts

- "What needs me today in Sniffington?"
- "Sniff Fernbill and tell me what people complain about."
- "List this week's negative mentions for Ledgerline and mark the double-billing ones as follow-up."
- "Which platform brought us the most mentions this month?"
