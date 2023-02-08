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
      menu: 0,
      account: false
    }
  },
  methods: {
    listenInput(event) {
      const { value } = event.target
      this.search = value;
    },
    listenMenu(n) {
      this.menu = n
    },
    listenAccount() {
      this.account = !this.account
    }
  }
}
</script>

<template>
  <Header @listenInput="listenInput" :search="search" @listenMenu="listenMenu" :menu="menu" :account="account" @listenAccount="listenAccount" />
  <div class="container-page">
    <Menu />
    <RouterView />
  </div>
  <Login @listenMenu="listenMenu" :menu="menu" :account="account" @listenAccount="listenAccount"/>
  <Signin @listenMenu="listenMenu" :menu="menu" />
  <div class="fondo__desplegable" :class="{ fondo__desplegable__active: menu }" @click="listenMenu(0)"></div>
</template>

