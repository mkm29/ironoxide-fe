<template>
  <header class="hdr">
    <div class="shell">
      <NuxtLink to="/" class="brand" aria-label="Iron Oxide home">
        <svg viewBox="0 0 64 64" aria-hidden="true">
          <defs>
            <linearGradient id="lr" x1="0" y1="0" x2="1" y2="1">
              <stop offset="0%" stop-color="#E0563E"/>
              <stop offset="100%" stop-color="#9F2A1A"/>
            </linearGradient>
          </defs>
          <path d="M32 11 L51 21.5 L51 42.5 L32 53 L13 42.5 L13 21.5 Z" fill="none" stroke="url(#lr)" stroke-width="2.25" stroke-linejoin="round"/>
          <text x="32" y="37" text-anchor="middle" font-size="13" font-family="ui-monospace, monospace" font-weight="700" fill="#E0563E" letter-spacing="-0.3">Fe<tspan font-size="8" baseline-shift="sub">2</tspan>O<tspan font-size="8" baseline-shift="sub">3</tspan></text>
          <g fill="#E0563E"><circle cx="32" cy="11" r="1.5"/><circle cx="51" cy="21.5" r="1.5"/><circle cx="51" cy="42.5" r="1.5"/><circle cx="32" cy="53" r="1.5"/><circle cx="13" cy="42.5" r="1.5"/><circle cx="13" cy="21.5" r="1.5"/></g>
        </svg>
        <span class="name">Iron Oxide</span>
      </NuxtLink>

      <nav class="nav">
        <NuxtLink to="/architecture">Architecture</NuxtLink>
        <NuxtLink to="/docs">Docs</NuxtLink>
        <NuxtLink to="/changelog">Changelog</NuxtLink>
        <a href="https://github.com/mkm29/ironoxide" target="_blank" rel="noopener">GitHub</a>
      </nav>

      <NuxtLink to="/#access" class="cta">
        Request access
        <svg width="12" height="12" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="square" aria-hidden="true"><path d="M3 8h10M9 4l4 4-4 4"/></svg>
      </NuxtLink>
    </div>
  </header>
</template>

<style scoped>
.hdr {
  position: sticky; top: 0; z-index: 50;
  background: rgba(11,12,15,0.78);
  backdrop-filter: saturate(140%) blur(8px);
  border-bottom: 1px solid var(--io-line);
}
.shell {
  max-width: 1180px;
  margin: 0 auto;
  padding: 14px 32px;
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 32px;
}
.brand { display: flex; align-items: center; gap: 10px; text-decoration: none; color: var(--io-text); }
.brand svg { width: 28px; height: 28px; display: block; }
.brand .name { font: 600 14px/1 var(--io-font-display); letter-spacing: -0.005em; }

.nav { display: flex; gap: 22px; justify-content: center; }
.nav a {
  font: 500 13px/1 var(--io-font-body);
  color: var(--io-text-muted);
  text-decoration: none;
  transition: color var(--io-dur-1) var(--io-ease);
}
.nav a:hover { color: var(--io-text); }
.nav a.router-link-active { color: var(--io-text); }

.cta {
  display: inline-flex; align-items: center; gap: 6px;
  background: var(--io-rust-500);
  color: #fff;
  border: 1px solid var(--io-rust-600);
  border-radius: var(--io-r-2);
  padding: 8px 14px;
  font: 600 12px/1 var(--io-font-display);
  letter-spacing: -0.005em;
  text-decoration: none;
  box-shadow: 0 1px 0 rgba(0,0,0,.4), inset 0 1px 0 rgba(255,255,255,.12);
  transition: background var(--io-dur-1) var(--io-ease), box-shadow var(--io-dur-1) var(--io-ease);
}
.cta:hover { background: var(--io-rust-600); box-shadow: var(--io-shadow-glow); }

@media (max-width: 760px) {
  .shell { grid-template-columns: auto auto; }
  .nav { display: none; }
}
</style>
