<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Aside from './components/Aside.vue'
import Login from './components/Login.vue'
import Signin from './components/Signin.vue'
</script>

<script>
export default {
  data() {
    return {
      review: sessionStorage.getItem("review"),
      search: "",
      menu: 0,
      account: false,
      loading: false,
      API_CHECK: "http://127.0.0.1:3001/api/v1/",
    }
  },
  mounted() {
    this.callAPI()
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
    },
    selectReview(n) {
      sessionStorage.setItem("review", n)
      this.review = n
    },
    async callAPI() {
      try {
        this.loading = false
        const response = await fetch(this.API_CHECK)
        if (response.status === 200) {
          this.loading = true
        } else {
          throw new Error('La respuesta de la API no fue exitosa')
        }
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<template>
  <Header v-if="loading" @listenInput="listenInput" :search="search" @listenMenu="listenMenu" :menu="menu"
    :account="account" @listenAccount="listenAccount" />  
  <div v-if="loading" class="container-page">
    <Aside />
    <RouterView :search="this.search" :review="review" @selectReview="selectReview" />
  </div>
  <div v-else class="loading">
    <img class="loading__logo" src="/src/assets/img/logo.svg" alt="Imagen del logo" />
    <div class="loading__effect"><div></div><div></div></div>
    <p class="loading__text">Se está conectando con el servidor</p>
  </div>
  <Login @listenMenu="listenMenu" :menu="menu" :account="account" @listenAccount="listenAccount" v-if="menu == 1" />
  <Signin @listenMenu="listenMenu" :menu="menu" v-if="menu == 2" />
  <div class="popup__bg" :class="{ popup__bg__active: menu }" @click="listenMenu(0)"></div>
</template>

