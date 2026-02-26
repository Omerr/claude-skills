---
marp: true
theme: default
size: 16:9
---

<style>
section {
  background: #1e1e1e;
  color: #d4d4d4;
  font-family: 'Cascadia Code', 'Fira Code', 'Consolas', monospace;
  font-size: 18px;
  padding: 40px 50px;
}
.prompt { color: #6a9955; }
.cmd { color: #dcdcaa; }
.question { color: #9cdcfe; font-weight: bold; }
.answer { color: #ce9178; }
.dim { color: #666; }
</style>

<span class="prompt">~/projects/my-app $</span> <span class="cmd">claude</span>

<span class="prompt">></span> <span class="cmd">/create-marp-deck API rate limiting</span>

<span class="dim">───────────────────────────────────────────────────────</span>

<span class="question">What's this presentation about? What should the audience walk away knowing?</span>

<span class="answer">How our rate limiting works, which algorithm we chose and why,
and what they need to know to configure it for their services.</span>

<span class="question">Who's the audience?</span>

<span class="answer">Platform engineering team — they know our stack but haven't
seen the rate limiting internals.</span>

<span class="question">What are the key points or sections you want to cover?</span>

<span class="answer">1. Why we need rate limiting (the incident last month)
2. Token bucket vs sliding window — our decision
3. How to configure it per-service
4. Monitoring dashboard walkthrough</span>
