<template>
  <div class="page-shell">
    <header class="hd">
      <span class="eyebrow">Docs</span>
      <h1>Install, boot, point your editor.</h1>
      <p class="lede">Five minutes from <code>brew install</code> to your first local token.</p>
    </header>

    <section v-for="b in blocks" :key="b.title" class="block">
      <h2>{{ b.title }}</h2>
      <p>{{ b.body }}</p>
      <pre v-if="b.code"><code>{{ b.code }}</code></pre>
    </section>
  </div>
</template>

<script setup>
useHead({ title: 'Docs — Iron Oxide' })
const blocks = [
  { title: 'Install', body: 'Homebrew tap. Mac only for now (M-series).', code: 'brew tap ironoxide/tap\nbrew install ironoxide' },
  { title: 'Boot the microVM', body: 'First boot pulls the golden image (~1.2GB). Subsequent boots are instant.', code: 'ironoxide up' },
  { title: 'Pull a model', body: 'Models land in ~/models inside the VM. The host mounts it read-only.', code: 'ironoxide pull qwen2.5-coder-32b' },
  { title: 'Point your editor', body: 'Anything that speaks the OpenAI HTTP format works. OpenCode, Cursor, Continue, your own tool.', code: 'export OPENAI_BASE_URL=http://localhost:47474/v1\nopencode' }
]
</script>

<style scoped>
.page-shell { max-width: 760px; margin: 0 auto; padding: 80px 32px; }
.hd { margin-bottom: 48px; }
.eyebrow { font: 500 10.5px/1 var(--io-font-mono); letter-spacing: .12em; text-transform: uppercase; color: var(--io-rust-500); }
h1 { font: 600 44px/1.05 var(--io-font-display); letter-spacing: -0.02em; margin: 12px 0 18px; }
.lede { font: 400 16px/1.55 var(--io-font-body); color: var(--io-text-muted); }
.lede code, .block code { font-family: var(--io-font-mono); }

.block { padding: 24px 0; border-top: 1px solid var(--io-line); }
.block:first-of-type { border-top: none; }
h2 { font: 600 22px/1.2 var(--io-font-display); margin: 0 0 8px; letter-spacing: -0.01em; }
.block p { font: 400 14.5px/1.55 var(--io-font-body); color: var(--io-text-muted); margin: 0 0 14px; max-width: 60ch; }
pre { background: var(--io-surface); border: 1px solid var(--io-line); border-radius: var(--io-r-2); padding: 16px 18px; margin: 0; overflow-x: auto; }
pre code { font: 400 13px/1.65 var(--io-font-mono); color: var(--io-text); background: none; border: none; padding: 0; }
</style>
