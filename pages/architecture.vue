<template>
  <div class="page-shell">
    <header class="hd">
      <span class="eyebrow">Architecture</span>
      <h1>How a request travels.</h1>
      <p class="lede">A drawn-out version of the diagram on the home page. Each box is a real process or store. The dotted line is the only place host and guest exchange privileged calls.</p>
    </header>

    <ol class="steps">
      <li v-for="(s, i) in steps" :key="i">
        <div class="num">{{ String(i+1).padStart(2,'0') }}</div>
        <div>
          <h3>{{ s.title }}</h3>
          <p>{{ s.body }}</p>
          <code v-if="s.code">{{ s.code }}</code>
        </div>
      </li>
    </ol>
  </div>
</template>

<script setup>
useHead({ title: 'Architecture — Iron Oxide' })
const steps = [
  { title: 'OpenCode opens a session', body: 'Your editor or shell speaks plain HTTP to localhost:47474. The agent runs on the host — no containers on your laptop.', code: 'POST http://localhost:47474/v1/chat' },
  { title: 'krunkit hands off to the microVM', body: 'libkrun wraps the request. The VM is already warm; cold boot is 800ms but you only pay it once.' },
  { title: 'llama-server picks up the prompt', body: 'Inside the guest, llama-server resolves the model from ~/models (read-only mount) and starts decoding.', code: '~/models/qwen2.5-coder-32b' },
  { title: 'Vulkan dispatches to Metal', body: 'Venus serializes Vulkan calls. virglrenderer translates them to Metal on the host. The guest never sees Apple silicon directly.' },
  { title: 'Tokens stream back', body: 'Server-sent events flow back through the same HTTP pipe. OpenCode streams tokens to your editor.' }
]
</script>

<style scoped>
.page-shell { max-width: 820px; margin: 0 auto; padding: 80px 32px; }
.hd { margin-bottom: 56px; }
.eyebrow { font: 500 10.5px/1 var(--io-font-mono); letter-spacing: .12em; text-transform: uppercase; color: var(--io-rust-500); }
h1 { font: 600 48px/1.05 var(--io-font-display); letter-spacing: -0.02em; margin: 12px 0 18px; }
.lede { font: 400 16px/1.55 var(--io-font-body); color: var(--io-text-muted); max-width: 60ch; }
.steps { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 28px; }
.steps li { display: grid; grid-template-columns: 56px 1fr; gap: 20px; padding: 20px; border: 1px solid var(--io-line); border-radius: var(--io-r-3); background: var(--io-surface); }
.num { font: 600 14px/1 var(--io-font-mono); color: var(--io-rust-500); letter-spacing: .04em; }
h3 { font: 600 17px/1.2 var(--io-font-display); margin: 0 0 6px; }
.steps p { font: 400 14px/1.55 var(--io-font-body); color: var(--io-text-muted); margin: 0 0 8px; }
code { font: 500 12.5px/1 var(--io-font-mono); color: var(--io-text); background: var(--io-bg); border: 1px solid var(--io-line); border-radius: 4px; padding: 4px 8px; display: inline-block; }
</style>
