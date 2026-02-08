# Building a code review agent that learns from feedback

There are plenty of AI code review tools now - Claude Code is getting impressively good at it. So why build my own?

Code review isn't just about catching bugs. It's how teams share knowledge about both code patterns and domain logic. If agents are becoming team members, I want to explore whether agentic code review can learn "our ways" - not just find security issues, but internalize why we do things a certain way.

## The Memory Problem

I've noticed agents remember things wrong - insisting on patterns I explicitly said not to use, or forgetting context from three PRs ago. For code review, bad memories are worse than no memories. The agent needs to remember the *right* lessons.

## What I'm Building

**Code Review Mentat** (CRM) - a CLI tool that:
1. Gathers deeper context using the Atlassian MCP server (pulls linked Jira tickets, Confluence docs)
2. Runs Claude Code to review PRs with that business context
3. Lets you triage each comment - apply fixes via Claude Code, post to the PR, reject it, or turn it into a memory for future reviews

The workflow: you review CRM's comments one by one, flagging particularly useful ones ("always do this in situations like X") or bad takes ("never suggest this again"). Over time, the agent learns what matters for your project and your team.

## The Hard Part: Creating Useful Memory

My current approach: when you flag a comment as memorable, CRM captures the comment, code snippet, and any context from Jira/Confluence. Then it generates a "situation description" - when should this lesson apply? That description gets stored with the lesson itself.

For retrieval, I'm building up in phases:

**Phase 0 (now):** Text search in SQLite with FTS5. If keyword matching ("async", "payment processing", "error handling") gets me 80% of the way there, maybe I don't need anything fancier.

**Phase 1 (next):** Semantic search with sqlite-vec and embeddings. This should catch similar situations even when worded differently - "handle failures" vs "error recovery" vs "graceful degradation".

I'm also testing *when* to retrieve memories:
- **Before review:** Scan the PR's changes and predict what situations might come up, then pull relevant memories upfront
- **During review:** Give Claude Code a memory search tool it can call as it reviews, so it fetches context only when needed

The first approach gives Claude more context from the start. The second is more targeted but risks the agent either ignoring the tool or overusing it.

Right now, everything runs locally in SQLite - no external dependencies, no separate services. Just a database file that grows as you teach it.

## What's Next 
Starting with the simplest thing that could work: keyword search in past comments. Then I'll see where it breaks and iterate from there. I'll be documenting what I learn - including the dead ends and surprises. If you're curious about teaching agents to think like your team, follow along.
