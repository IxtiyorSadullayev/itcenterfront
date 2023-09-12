<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      
      <nav>
        <RouterLink class="nav-link" to="/">Home</RouterLink>
        <RouterLink class="nav-link" to="/teachers">Ishchilar</RouterLink>
        <RouterLink class="nav-link" to="/students">O'quvchilar</RouterLink>
        <RouterLink class="nav-link" to="/groups">O'quv guruhlari</RouterLink>
        <RouterLink class="nav-link" to="/story">O'quv jarayoni tarixi</RouterLink>
        <RouterLink class="nav-link" to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

header {
  line-height: 1.5;
  max-height: 100vh;
  width: 20%;
  background-color: rgba(0, 255, 255, 0.082);
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
}

.nav-link.router-link-exact-active {
  display: block;
  color: var(--color-text);
}
.nav-link{
  display: block;
  color: var(--color-text);
  padding: 10px 0;
}
nav a.router-link-exact-active:hover {
  background-color: transparent;
  display: block;
}
.nav-link.router-link-active{
  display: block;
  padding: 10px 0;
  background-color: rgba(0, 255, 255, 0.301);
}

</style>
