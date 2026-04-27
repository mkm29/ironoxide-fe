<template>
  <div class="app">
    <SiteHeader />
    <main class="page"><slot /></main>
    <SiteFooter />
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-image:
    radial-gradient(ellipse at 80% -10%, rgba(224,86,62,0.06), transparent 55%),
    radial-gradient(ellipse at 0% 110%, rgba(31,79,160,0.06), transparent 55%);
}
.page { flex: 1; }
</style>
