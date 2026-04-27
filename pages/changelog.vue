<template>
  <div class="page-shell">
    <header class="hd">
      <span class="eyebrow">Changelog</span>
      <h1>What's shipped.</h1>
      <p class="lede">Verb-first, past tense. The honest list.</p>
    </header>

    <ol class="log">
      <li v-for="r in releases" :key="r.version">
        <header class="row">
          <span class="ver">{{ r.version }}</span>
          <span class="date">{{ r.date }}</span>
        </header>
        <ul>
          <li v-for="(line, i) in r.lines" :key="i" :class="line.kind">
            <span class="tag">{{ line.kind }}</span>
            <span>{{ line.text }}</span>
          </li>
        </ul>
      </li>
    </ol>
  </div>
</template>

<script setup>
useHead({ title: 'Changelog — Iron Oxide' })
const releases = [
  { version: 'v0.4.0', date: '2025-03-14', lines: [
    { kind: 'Added', text: 'GPU passthrough on M3/M4 via Venus + virglrenderer.' },
    { kind: 'Added', text: 'ironoxide pull for models hosted on Hugging Face mirrors.' },
    { kind: 'Cut',   text: 'Bundled Ollama wrapper. Use llama-server directly.' }
  ]},
  { version: 'v0.3.0', date: '2025-02-02', lines: [
    { kind: 'Added', text: 'Golden image build: ironoxide.raw, 1.2GB.' },
    { kind: 'Fixed', text: 'Cold boot regression on libkrun 1.9 (now 800ms).' }
  ]},
  { version: 'v0.2.0', date: '2025-01-08', lines: [
    { kind: 'Added', text: 'OpenCode integration on port 47474.' },
    { kind: 'Fixed', text: 'Read-only mount of ~/models from host.' }
  ]}
]
</script>

<style scoped>
.page-shell { max-width: 720px; margin: 0 auto; padding: 80px 32px; }
.hd { margin-bottom: 48px; }
.eyebrow { font: 500 10.5px/1 var(--io-font-mono); letter-spacing: .12em; text-transform: uppercase; color: var(--io-rust-500); }
h1 { font: 600 44px/1.05 var(--io-font-display); letter-spacing: -0.02em; margin: 12px 0 18px; }
.lede { font: 400 16px/1.55 var(--io-font-body); color: var(--io-text-muted); }

.log { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 36px; }
.log > li { border: 1px solid var(--io-line); border-radius: var(--io-r-3); background: var(--io-surface); overflow: hidden; }
.row { display: flex; justify-content: space-between; align-items: baseline; padding: 16px 20px; border-bottom: 1px solid var(--io-line); background: var(--io-surface-2); }
.ver { font: 600 14px/1 var(--io-font-mono); color: var(--io-text); }
.date { font: 500 11px/1 var(--io-font-mono); color: var(--io-text-dim); letter-spacing: .04em; }
.log ul { list-style: none; padding: 12px 20px; margin: 0; }
.log ul li { display: grid; grid-template-columns: 80px 1fr; gap: 12px; padding: 8px 0; align-items: baseline; }
.tag { font: 500 10.5px/1 var(--io-font-mono); letter-spacing: .08em; text-transform: uppercase; color: var(--io-text-dim); }
.log li.Added .tag { color: var(--io-ok); }
.log li.Fixed .tag { color: var(--io-blue-300); }
.log li.Cut .tag { color: var(--io-rust-500); }
.log ul li > span:last-child { font: 400 13.5px/1.5 var(--io-font-body); color: var(--io-text-muted); }
</style>
