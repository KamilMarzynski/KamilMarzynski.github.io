# My AI toolset snapshot

When my previous company got Cursor licenses, I ran into a practical problem fast. My team was responsible for over 20 microservices, and other teams often worked in the same repositories — so keeping shared prompt files in version control wasn't really an option. Distributing them manually across that many repos would have been a maintenance nightmare. At the time I was leading the team, and finding a way to give everyone the same setup without extra overhead was something I kept thinking about.

The solution I landed on was a local MCP server distributed via Git. Anyone could pull the latest version and build it — no copying files, no manual syncing, and the whole thing was versioned. But the interesting part was what it actually exposed. Instead of tools like "create Jira ticket" that do something, it exposed things like `setup_branch_for_development` or `prepare_QA_documentation` — instructions that told the agent where to find request/response schemas, how RabbitMQ message definitions were organized, what our branching rules were, that each microservice might run on a different Node.js version and should be tested accordingly. Context the agent needed to do useful work in our system. Looking back, these were skills. We just didn't have that word for them yet.

## Research and notes: Perplexity + Obsidian

My main research stack is Perplexity combined with Obsidian. I use Perplexity — and their browser, Comet — for almost everything, but where it really shines is producing clean documentation from research. I keep all of that in Obsidian, a notes app built around a local file system and plain Markdown files.

Markdown files are surprisingly good sources of knowledge for AI agents. Obsidian has become my bridge between Perplexity and my second main tool: Claude.

## Writing code: Claude Code + Cowork

Claude picks up where Perplexity leaves off — it helps me digest research and translate it into code. I use it two ways.

The first is Claude Code, which is probably obvious. My preferred setup is Claude Code with a small set of skills from [Superpowers](https://github.com/obra/superpowers). It's a short list, but those skills make a real difference. I recently used this setup to build a general-purpose TypeScript library [ts-mapper-tracer](https://github.com/KamilMarzynski/ts-mapper-tracer) that solves a model mapping problem we have at my current company — a deeper technical breakdown of that is coming in a separate post.

The second is Claude Cowork, which is less obvious. Cowork can be launched from Projects, which are spaces where you can gather documentation, build memory around a topic, and collect related chats in one place. I use this to move research context directly into a coding session: gather data with Perplexity, refine it with Claude in a project, then move to Cowork to start implementing or continue in Claude Code. The cycle repeats from there.

Perplexity has a similar concept called Spaces, where chats and materials are grouped by topic. My Claude projects and Perplexity spaces usually mirror each other.

## Writing: humanizer skill

I also use Claude to clean up and proofread posts before publishing. That probably goes without saying. But there's one thing worth calling out: the [humanizer](link) skill. It does a good job catching AI-sounding phrasing that sneaks in, even when you're the one writing.

## What's next

The toolset I described here is mostly about research and coding. But lately I've been pulling Claude into something more personal. Cowork's [scheduled tasks](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-cowork) — tasks you write once and Claude runs automatically at whatever cadence you choose — turned out to be what I was missing. I have scheduled summaries of my labeled inbox, daily blog roundups, and a task that lets me assign work to Claude directly from Obsidian. The idea is to make Obsidian not just a place where I organize notes, but a place where I can hand things off and come back to results.

It's still a work in progress, but it's the thing I'm most excited about right now. More on that in the next post.
