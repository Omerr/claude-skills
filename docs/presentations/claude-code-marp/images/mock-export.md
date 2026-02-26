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
.info { color: #569cd6; }
.file { color: #ce9178; }
.dim { color: #666; }
.check { color: #4ec9b0; }
</style>

<span class="prompt">~/projects/my-app $</span> <span class="cmd">marp --no-stdin presentations/api-rate-limiting.md -o presentations/api-rate-limiting.html</span>

<span class="info">[  INFO ]</span> Converting 1 markdown...
<span class="info">[  INFO ]</span> api-rate-limiting.md => <span class="file">api-rate-limiting.html</span>

<span class="prompt">~/projects/my-app $</span> <span class="cmd">marp --no-stdin --pptx presentations/api-rate-limiting.md -o presentations/api-rate-limiting.pptx</span>

<span class="info">[  INFO ]</span> Converting 1 markdown...
<span class="info">[  INFO ]</span> api-rate-limiting.md => <span class="file">api-rate-limiting.pptx</span>

<span class="prompt">~/projects/my-app $</span> <span class="cmd">ls presentations/</span>

<span class="file">api-rate-limiting.md</span>
<span class="file">api-rate-limiting.html</span>   <span class="check">✓</span> <span class="dim">open in browser, share via Slack</span>
<span class="file">api-rate-limiting.pptx</span>   <span class="check">✓</span> <span class="dim">open in PowerPoint, present anywhere</span>
