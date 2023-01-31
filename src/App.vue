<script setup>
  import { RouterLink, RouterView } from 'vue-router'
  import Home from './components/Home.vue'
  import Header from './components/Header.vue'
  
  // let search = null
</script>

<template>
  <Header search="search"/>
  <header>
    <div class="wrapper">
      <Home />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>