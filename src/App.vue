<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
import Login from './components/Login.vue'

</script>

<script>
export default {
  data() {
    return {
      search: "",
      menu: false
    }
  },
  methods: {
    listenInput(event) {
      const { value } = event.target
      this.search = value;
    },
    listenMenu() {
      this.menu = !this.menu
    }
  }
}
</script>

<template>
  <Header @listenInput="listenInput" :search="search" @listenMenu="listenMenu" :menu="menu" />
  <div class="container-page">
    <Menu />
    <RouterView />
  </div>
  <Login @listenMenu="listenMenu" :menu="menu" />
  <div class="fondo__desplegable" :class="{ fondo__desplegable__active: menu }" @click="listenMenu"></div>
</template>

