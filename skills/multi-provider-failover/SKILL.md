---
name: "multi-provider-failover"
description: "Dynamic routing across 23 LLM providers, token compaction, and transparent error failover."
---

# Multi-Provider Failover Skill

## Overview
Manages resilient inference across cloud and local model providers, monitoring latency, token budgets, and rate limit errors.

## Failover Strategy
1. **Provider Health Assessment**: Track response latency and rate limit headers across supported providers.
2. **Context Compaction**: When conversation history approaches token capacity, summarize older turns before inference.
3. **Transparent Fallback**: On HTTP 429, 502, or timeout errors, seamlessly redirect the payload to the next configured fallback provider.
4. **Cost & Latency Optimization**: Direct routine tasks to lightweight local models and complex reasoning to frontier models.
