<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
import Login from './components/Login.vue'
import Signin from './components/Signin.vue'

</script>

<script>
export default {
  data() {
    return {
      search: "",
      menu: 0
    }
  },
  methods: {
    listenInput(event) {
      const { value } = event.target
      this.search = value;
    },
    listenMenu(n) {
      this.menu = n
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
  <Signin @listenMenu="listenMenu" :menu="menu" />
  <div class="fondo__desplegable" :class="{ fondo__desplegable__active: menu }" @click="listenMenu(0)"></div>
</template>

