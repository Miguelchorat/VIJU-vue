<script setup>
  import { RouterView } from 'vue-router'
  import Header from './components/Header.vue'
  import Menu from './components/Menu.vue'
</script>

<script>
  export default {
    data () {
      return {
        search: "",
      }
    },
  }
</script>

<template>
  <Header :search="search" />
  <p>{{ search }}</p>
  <div class="container-page">
    <Menu />  
    <RouterView />
  </div>
</template>

