---
layout: post
title: "Why isn't ours reliable enough to trust at scale?"
date: 2026-03-29
tags: [agents, evals, observability]
excerpt: "The question in 2025 was: should we build agents? The question in 2026 is: why isn't ours reliable enough to trust at scale? LangChain's 2026 State of Agent Engineering survey reveals quality is the #1 production killer, and we're still flying blind on evals."
---

The question in 2025 was: **should we build agents?**

The question in 2026 is: **why isn't ours reliable enough to trust at scale?**

LangChain's 2026 State of Agent Engineering survey (1,300+ professionals) found **57% of orgs now have agents in production** — up from 51% last year. The conversation has moved from demos to deployments.

But the problems have moved too.

**Quality is the #1 production killer (32%), not cost.** And here's the stat that should bother everyone building in this space:

→ **Observability adoption: 89%**  
→ **Offline evals adoption: 52%**  
→ **Online evals adoption: 37%**

*(Source: LangChain, State of Agent Engineering 2026)*

We're great at logging what happened. We're still treating evals as optional.

As LangChain's January 2026 newsletter put it: **traditional software treats tracing and testing as separate — with agents, they're inseparable.** Production traces become test cases. Evaluation suites grow continuously from real-world failures.

## The Winning Pattern

The teams winning in production aren't running the smartest models. They're the ones who've closed the loop:

1. **Trace every agent run in production**
2. **Flag anomalous/failed runs automatically**
3. **Route failures back into offline eval datasets**
4. **Iterate on prompts, tools, and routing logic with that data**

Without steps 3 and 4, you're flying blind between deployments.

## Architecture: The Puppeteer Pattern

Architecturally, the **"puppeteer" pattern** — a central orchestrator + specialized sub-agents — is becoming the production default (LangGraph leading the way). Bounded scope is more debuggable. Same lesson microservices taught us a decade ago.

## Key Insights

- **Why LLM-as-judge is dominating:** 53% adoption because it scales human judgment
- **Why online evals jump to 45% once you hit production:** Real data forces you to test
- **What the closed-loop eval pattern looks like in practice:** Continuous feedback loops from production

---

**What's the biggest eval or observability challenge in your agent stack right now?** Let me know in the comments or reach out on LinkedIn.
