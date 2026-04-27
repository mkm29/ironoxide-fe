<template>
  <footer class="ftr">
    <div class="shell">
      <div class="left">© Iron Oxide · MIT</div>
      <nav class="links">
        <a href="#">github</a>
        <a href="#">docs</a>
        <a href="#">changelog</a>
        <a href="#">x</a>
      </nav>
    </div>
  </footer>
</template>

<style scoped>
.ftr {
  border-top: 1px solid var(--io-line);
  margin-top: 80px;
}
.shell {
  max-width: 1180px;
  margin: 0 auto;
  padding: 28px 32px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: var(--io-text-faint);
  font: 500 10.5px/1 var(--io-font-mono);
  letter-spacing: .08em;
  text-transform: uppercase;
}
.links { display: flex; gap: 22px; }
.links a { color: var(--io-text-dim); text-decoration: none; }
.links a:hover { color: var(--io-text); }
</style>
