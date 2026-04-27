<template>
  <div class="home">
    <!-- HERO -->
    <section class="hero">
      <div class="shell">
        <span class="pill"><span class="dot"></span>v0 · private beta</span>
        <h1>Run frontier models <span class="accent">locally</span>, on <span class="blue">Apple silicon</span>.</h1>
        <p class="lede">A hardened Linux microVM with GPU passthrough, a coding agent, and a golden image you boot in under a second. Models stay on your machine. Code stays on your machine. Talk to <code>llama-server</code> over HTTP.</p>

        <div class="cta-row">
          <a href="#access" class="btn primary">
            Request access
            <svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="square"><path d="M3 8h10M9 4l4 4-4 4"/></svg>
          </a>
          <NuxtLink to="/docs" class="btn ghost">Read the docs</NuxtLink>
        </div>

        <div class="specs">
          <div><div class="k">Cold boot</div><div class="v">800<span class="u">ms</span></div></div>
          <div><div class="k">Image</div><div class="v">~1.2<span class="u">GB</span></div></div>
          <div><div class="k">Target</div><div class="v">M-series<span class="u"> · 40c</span></div></div>
          <div><div class="k">Default port</div><div class="v">47474</div></div>
        </div>
      </div>
    </section>

    <!-- WHAT'S IN THE BOX -->
    <section class="section">
      <div class="shell">
        <div class="section-head">
          <span class="eyebrow">What's in the image</span>
          <h2>Three things that don't normally play nicely together.</h2>
        </div>
        <div class="grid-3">
          <article class="card" v-for="f in features" :key="f.title">
            <div class="card-mono">{{ f.id }}</div>
            <h3>{{ f.title }}</h3>
            <p>{{ f.body }}</p>
            <ul class="kv">
              <li v-for="row in f.rows" :key="row[0]">
                <span class="k">{{ row[0] }}</span>
                <span class="v">{{ row[1] }}</span>
              </li>
            </ul>
          </article>
        </div>
      </div>
    </section>

    <!-- ARCH DIAGRAM -->
    <section class="section">
      <div class="shell">
        <div class="section-head">
          <span class="eyebrow">Architecture</span>
          <h2>The trust boundary, drawn honestly.</h2>
        </div>

        <div class="diagram">
          <div class="lane">
            <div class="lane-label">Host · macOS</div>
            <div class="node host">
              <div class="node-title">OpenCode</div>
              <div class="node-sub">agent · port 47474</div>
            </div>
            <div class="node host">
              <div class="node-title">krunkit</div>
              <div class="node-sub">VMM · libkrun</div>
            </div>
          </div>

          <div class="boundary">
            <span>trust boundary · Venus / virglrenderer</span>
          </div>

          <div class="lane">
            <div class="lane-label">Guest · Linux microVM</div>
            <div class="node guest accent">
              <div class="node-title">llama-server</div>
              <div class="node-sub">HTTP · /v1/chat</div>
            </div>
            <div class="node guest">
              <div class="node-title">Vulkan</div>
              <div class="node-sub">→ Metal passthrough</div>
            </div>
            <div class="node guest cyl">
              <div class="node-title">~/models</div>
              <div class="node-sub">read-only mount</div>
            </div>
          </div>
        </div>

        <p class="diagram-foot">Solid boxes are processes. Cylinders are stores. The dotted line is the only place the host and guest exchange privileged calls — everything else is HTTP.</p>
      </div>
    </section>

    <!-- TERMINAL -->
    <section class="section">
      <div class="shell">
        <div class="section-head">
          <span class="eyebrow">Quickstart</span>
          <h2>Boot, pull a model, point your editor.</h2>
        </div>
        <div class="terminal">
          <div class="term-bar">
            <span class="dot d-r"></span><span class="dot d-y"></span><span class="dot d-g"></span>
            <span class="term-title">~/projects/iron-oxide — zsh</span>
          </div>
          <pre class="term-body"><span class="prompt">$</span> ironoxide up
<span class="ok">✓</span> golden image <span class="muted">ironoxide.raw (1.2GB)</span>
<span class="ok">✓</span> microVM up <span class="muted">in 812ms</span>
<span class="ok">✓</span> GPU passthrough <span class="muted">Metal &lt;- Vulkan</span>
<span class="ok">✓</span> llama-server <span class="muted">listening on :47474</span>

<span class="prompt">$</span> ironoxide pull qwen2.5-coder-32b
  pulling      <span class="rust">████████████████████</span>  4.2GB / 4.2GB
<span class="ok">✓</span> verified sha256 <span class="muted">a1c4…9f2b</span>

<span class="prompt">$</span> export OPENAI_BASE_URL=http://localhost:47474/v1
<span class="prompt">$</span> opencode</pre>
        </div>
      </div>
    </section>

    <!-- ACCESS FORM -->
    <section id="access" class="section">
      <div class="shell access-grid">
        <div>
          <span class="eyebrow">Private beta</span>
          <h2>Get an invite.</h2>
          <p class="lede">We're letting people in as we harden the trust boundary. No spam, one email when your seat opens.</p>
        </div>
        <div class="panel">
          <form @submit.prevent="submit" :class="{ sent }">
            <div class="field">
              <label for="email">Email</label>
              <input id="email" v-model="email" type="email" required placeholder="you@workstation.local"/>
            </div>
            <div class="field">
              <label for="role">You build</label>
              <select id="role" v-model="role">
                <option>Backend / infra</option>
                <option>ML / model serving</option>
                <option>Frontend / agents</option>
                <option>Security / platform</option>
                <option>Just curious</option>
              </select>
            </div>
            <div class="checks">
              <label class="check"><input type="checkbox" v-model="optReleases"/><span>Release notes</span></label>
              <label class="check"><input type="checkbox" v-model="optBeta"/><span>Beta invites</span></label>
            </div>
            <button class="btn primary" type="submit">
              Request access
              <svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="square"><path d="M3 8h10M9 4l4 4-4 4"/></svg>
            </button>
            <p class="fineprint">By signing up you agree to our <a href="#">terms</a> · <a href="#">privacy</a>.</p>
            <div v-if="sent" class="success">
              <span class="badge"></span>
              <div><strong>You're on the list.</strong><br/>We'll send a single email when your invite is ready.</div>
            </div>
          </form>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const features = [
  {
    id: '01 · microVM',
    title: 'Hardened Linux microVM',
    body: 'krunkit + libkrun. Boots from a single golden image. No installer, no orchestrator, no daemon.',
    rows: [['Kernel', 'libkrun'], ['Image', 'ironoxide.raw'], ['Cold boot', '~800ms']]
  },
  {
    id: '02 · GPU',
    title: 'GPU passthrough',
    body: 'Vulkan inside the guest, Metal on the host. Venus + virglrenderer serialize the trust boundary.',
    rows: [['Guest API', 'Vulkan'], ['Host API', 'Metal'], ['Bridge', 'Venus']]
  },
  {
    id: '03 · Agent',
    title: 'Coding agent included',
    body: 'OpenCode talks HTTP to llama-server. Drop-in OPENAI_BASE_URL. Bring your own editor.',
    rows: [['Agent', 'OpenCode'], ['Server', 'llama-server'], ['Port', '47474']]
  }
]

const email = ref('')
const role = ref('Backend / infra')
const optReleases = ref(true)
const optBeta = ref(false)
const sent = ref(false)

function submit () {
  if (!email.value || !email.value.includes('@')) return
  sent.value = true
}
</script>

<style scoped>
.shell { max-width: 1180px; margin: 0 auto; padding: 0 32px; }

/* hero */
.hero { padding: 96px 0 80px;
  background-image: linear-gradient(var(--io-line) 1px, transparent 1px),
                    linear-gradient(90deg, var(--io-line) 1px, transparent 1px);
  background-size: 56px 56px, 56px 56px;
  background-position: -1px -1px;
  position: relative;
}
.hero::after {
  content: ""; position: absolute; inset: 0;
  background: radial-gradient(ellipse at 50% 30%, transparent 30%, var(--io-bg) 78%);
  pointer-events: none;
}
.hero .shell { position: relative; z-index: 1; max-width: 920px; }

.pill {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 6px 12px;
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-pill);
  background: var(--io-surface);
  font: 500 11px/1 var(--io-font-mono);
  letter-spacing: .08em; text-transform: uppercase;
  color: var(--io-text-muted);
}
.pill .dot { width: 6px; height: 6px; border-radius: 50%; background: var(--io-rust-500); animation: pulse 2.4s var(--io-ease) infinite; }
@keyframes pulse { 0%,100% { box-shadow: 0 0 0 0 rgba(224,86,62,.5);} 50% { box-shadow: 0 0 0 6px rgba(224,86,62,0);} }

h1 {
  font: 600 64px/1.02 var(--io-font-display);
  letter-spacing: -0.025em;
  margin: 18px 0 18px;
  text-wrap: balance;
}
h1 .accent { color: var(--io-rust-500); }
h1 .blue { color: var(--io-blue-500); }

.lede {
  font: 400 17px/1.55 var(--io-font-body);
  color: var(--io-text-muted);
  max-width: 60ch;
  margin: 0 0 28px;
  text-wrap: pretty;
}
.lede code {
  font: 500 13.5px/1 var(--io-font-mono);
  color: var(--io-text);
  background: var(--io-surface-2);
  border: 1px solid var(--io-line);
  border-radius: 4px;
  padding: 1px 6px;
}

.cta-row { display: flex; gap: 12px; margin-bottom: 36px; flex-wrap: wrap; }
.btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 12px 16px;
  border-radius: var(--io-r-2);
  font: 600 14px/1 var(--io-font-display);
  text-decoration: none;
  cursor: pointer;
  transition: background var(--io-dur-1) var(--io-ease), box-shadow var(--io-dur-1) var(--io-ease);
  border: 1px solid transparent;
}
.btn.primary {
  background: var(--io-rust-500);
  color: #fff;
  border-color: var(--io-rust-600);
  box-shadow: 0 1px 0 rgba(0,0,0,.4), inset 0 1px 0 rgba(255,255,255,.12);
}
.btn.primary:hover { background: var(--io-rust-600); box-shadow: var(--io-shadow-glow); }
.btn.ghost {
  background: transparent;
  color: var(--io-text);
  border-color: var(--io-line-strong);
}
.btn.ghost:hover { background: var(--io-surface); }

.specs {
  display: grid; grid-template-columns: repeat(4, 1fr); gap: 0;
  border: 1px solid var(--io-line); border-radius: var(--io-r-3);
  overflow: hidden; background: var(--io-surface);
  max-width: 720px;
}
.specs > div { padding: 14px 16px; border-right: 1px solid var(--io-line); }
.specs > div:last-child { border-right: none; }
.specs .k { font: 500 10px/1 var(--io-font-mono); letter-spacing: .12em; text-transform: uppercase; color: var(--io-text-dim); margin-bottom: 6px; }
.specs .v { font: 600 16px/1.1 var(--io-font-display); color: var(--io-text); }
.specs .v .u { font: 500 11px/1 var(--io-font-mono); color: var(--io-text-dim); margin-left: 2px; }

/* sections */
.section { padding: 72px 0; border-top: 1px solid var(--io-line); }
.section-head { margin-bottom: 40px; max-width: 720px; }
.eyebrow {
  font: 500 10.5px/1 var(--io-font-mono);
  letter-spacing: .12em; text-transform: uppercase;
  color: var(--io-rust-500);
}
h2 { font: 600 32px/1.15 var(--io-font-display); letter-spacing: -0.02em; margin: 12px 0 0; text-wrap: balance; }
h3 { font: 600 16px/1.2 var(--io-font-display); margin: 14px 0 8px; }

/* features */
.grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
.card {
  background: var(--io-surface);
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-3);
  padding: 20px;
}
.card-mono {
  font: 500 10.5px/1 var(--io-font-mono);
  color: var(--io-text-dim);
  letter-spacing: .08em; text-transform: uppercase;
}
.card p { font: 400 14px/1.55 var(--io-font-body); color: var(--io-text-muted); margin: 0 0 14px; }
.kv { list-style: none; padding: 0; margin: 0; border-top: 1px solid var(--io-line); }
.kv li { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px dashed var(--io-line); }
.kv li:last-child { border-bottom: none; }
.kv .k { font: 500 11px/1 var(--io-font-mono); color: var(--io-text-dim); letter-spacing: .06em; text-transform: uppercase; }
.kv .v { font: 500 12px/1 var(--io-font-mono); color: var(--io-text); }

/* diagram */
.diagram {
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-3);
  background: var(--io-surface);
  padding: 32px;
  display: flex; flex-direction: column; gap: 24px;
}
.lane { display: grid; grid-template-columns: 160px 1fr 1fr 1fr; gap: 16px; align-items: stretch; }
.lane-label {
  font: 500 10.5px/1 var(--io-font-mono);
  color: var(--io-text-dim); letter-spacing: .08em; text-transform: uppercase;
  align-self: center;
}
.node {
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-2);
  padding: 14px;
  background: var(--io-bg);
}
.node.host { border-color: var(--io-blue-700); }
.node.guest { border-color: var(--io-line-strong); }
.node.accent { border-color: var(--io-rust-600); box-shadow: var(--io-shadow-glow); }
.node.cyl { border-radius: 24px / 12px; }
.node-title { font: 600 13px/1.2 var(--io-font-mono); color: var(--io-text); }
.node-sub { font: 400 11px/1.3 var(--io-font-mono); color: var(--io-text-dim); margin-top: 4px; }
.boundary {
  border-top: 1px dashed var(--io-line-strong);
  text-align: center;
  position: relative;
  margin: 4px 0;
}
.boundary span {
  position: relative; top: -10px;
  background: var(--io-surface);
  padding: 0 12px;
  font: 500 10.5px/1 var(--io-font-mono);
  letter-spacing: .08em; text-transform: uppercase;
  color: var(--io-text-dim);
}
.diagram-foot {
  font: 400 13px/1.5 var(--io-font-body);
  color: var(--io-text-dim);
  margin: 16px 0 0;
  max-width: 60ch;
}

/* terminal */
.terminal {
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-3);
  background: var(--io-surface);
  overflow: hidden;
  box-shadow: var(--io-shadow-2);
}
.term-bar {
  display: flex; align-items: center; gap: 8px;
  padding: 10px 14px;
  border-bottom: 1px solid var(--io-line);
  background: var(--io-surface-2);
}
.term-bar .dot { width: 10px; height: 10px; border-radius: 50%; }
.d-r { background: #FF5F57; } .d-y { background: #FEBC2E; } .d-g { background: #28C840; }
.term-title {
  margin-left: 8px;
  font: 500 11px/1 var(--io-font-mono);
  color: var(--io-text-dim);
}
.term-body {
  margin: 0;
  padding: 20px 24px;
  font: 400 13.5px/1.7 var(--io-font-mono);
  color: var(--io-text);
  white-space: pre-wrap;
}
.term-body .prompt { color: var(--io-rust-500); }
.term-body .ok { color: var(--io-ok); }
.term-body .muted { color: var(--io-text-dim); }
.term-body .rust { color: var(--io-rust-500); }

/* access */
.access-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 64px; align-items: center; }
.panel {
  background: var(--io-surface);
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-4);
  padding: 28px;
  box-shadow: var(--io-shadow-2);
}
form { display: flex; flex-direction: column; gap: 14px; }
.field { display: flex; flex-direction: column; gap: 6px; }
label { font: 500 10.5px/1 var(--io-font-mono); letter-spacing: .08em; text-transform: uppercase; color: var(--io-text-dim); }
input[type=email], select {
  background: var(--io-bg);
  border: 1px solid var(--io-line);
  border-radius: var(--io-r-2);
  padding: 12px 14px;
  color: var(--io-text);
  font: 400 14px/1.2 var(--io-font-body);
  width: 100%;
  transition: border-color var(--io-dur-1) var(--io-ease), box-shadow var(--io-dur-1) var(--io-ease);
}
input[type=email]::placeholder { color: var(--io-text-faint); }
input:focus, select:focus { outline: none; border-color: var(--io-rust-500); box-shadow: 0 0 0 3px rgba(224,86,62,.15); }
select { appearance: none; padding-right: 36px;
  background-image: linear-gradient(45deg, transparent 50%, var(--io-text-dim) 50%), linear-gradient(135deg, var(--io-text-dim) 50%, transparent 50%);
  background-position: calc(100% - 18px) 50%, calc(100% - 13px) 50%;
  background-size: 5px 5px; background-repeat: no-repeat;
}
.checks { display: flex; gap: 18px; flex-wrap: wrap; }
.check { display: flex; align-items: center; gap: 8px; cursor: pointer; }
.check input { appearance: none; width: 14px; height: 14px; border: 1px solid var(--io-line-strong); border-radius: 3px; background: var(--io-bg); display: inline-grid; place-content: center; cursor: pointer; }
.check input::before { content: ""; width: 8px; height: 8px; transform: scale(0); transition: transform var(--io-dur-1) var(--io-ease); background: var(--io-rust-500); border-radius: 1px; }
.check input:checked { border-color: var(--io-rust-500); }
.check input:checked::before { transform: scale(1); }
.check span { font: 500 12px/1 var(--io-font-mono); color: var(--io-text-muted); }
.fineprint { font: 500 10.5px/1.5 var(--io-font-mono); color: var(--io-text-faint); margin: 4px 0 0; }
.fineprint a { color: var(--io-text-dim); text-decoration: none; border-bottom: 1px dotted var(--io-text-faint); }
.success { display: flex; gap: 12px; padding: 14px; border: 1px solid rgba(74,222,128,.35); background: rgba(74,222,128,.06); border-radius: var(--io-r-2); color: var(--io-text); font: 400 13px/1.5 var(--io-font-body); }
.success .badge { width: 18px; height: 18px; border-radius: 50%; background: var(--io-ok); flex: none; display: inline-grid; place-content: center; }
.success .badge::before { content: "✓"; color: #0B0C0F; font: 700 11px/1 var(--io-font-display); }
form.sent .field, form.sent .checks, form.sent button, form.sent .fineprint { display: none; }

@media (max-width: 860px) {
  h1 { font-size: 44px; }
  .grid-3 { grid-template-columns: 1fr; }
  .specs { grid-template-columns: repeat(2, 1fr); }
  .specs > div:nth-child(2) { border-right: none; }
  .lane { grid-template-columns: 1fr 1fr; }
  .lane-label { grid-column: 1 / -1; }
  .access-grid { grid-template-columns: 1fr; gap: 32px; }
}
</style>
