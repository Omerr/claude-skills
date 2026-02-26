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
.user { color: #dcdcaa; }
.claude { color: #9cdcfe; }
.dim { color: #666; }
.file { color: #ce9178; }
.diff-add { color: #4ec9b0; }
.diff-del { color: #f44747; }
</style>

<span class="prompt">></span> <span class="user">Slide 6 is too dense. Split the algorithm comparison into two slides — one for token bucket, one for sliding window.</span>

<span class="claude">I'll split slide 6 into two separate slides, one per algorithm.</span>

<span class="dim">  Edit </span><span class="file">presentations/api-rate-limiting.md</span>
<span class="dim">  ───────────────────────────────────────────</span>
<span class="diff-del">  - # Algorithm Comparison</span>
<span class="diff-del">  - | Feature | Token Bucket | Sliding Window |</span>
<span class="diff-add">  + # Token Bucket</span>
<span class="diff-add">  + Tokens refill at a steady rate...</span>
<span class="diff-add">  + ---</span>
<span class="diff-add">  + # Sliding Window</span>
<span class="diff-add">  + Track exact timestamp of every request...</span>

<span class="prompt">></span> <span class="user">Add a "Why we chose token bucket" callout to that first slide</span>

<span class="claude">Added a blockquote callout explaining the decision.</span>

<span class="dim">  Edit </span><span class="file">presentations/api-rate-limiting.md</span>
<span class="dim">  ───────────────────────────────────────────</span>
<span class="diff-add">  + > We chose token bucket because it handles bursty traffic</span>
<span class="diff-add">  + > from our mobile clients without penalizing steady callers</span>
