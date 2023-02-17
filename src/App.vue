<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Aside from './components/Aside.vue'
import Login from './components/Login.vue'
import Signin from './components/Signin.vue'
import axios from 'axios'
</script>

<script>
export default {
  data() {
    return {
      search: "",
      menu: 0,
      account: false,
      loading: false,
      userId: localStorage.getItem('userId') ?? 0,
      session: localStorage.getItem('session') ?? false,
      API_CHECK: "http://127.0.0.1:3001/api/v1/",
      API_LOGIN: "http://127.0.0.1:3001/api/v1/auth/",
      API_CLOSE: "http://127.0.0.1:3001/api/v1/auth/users/session="
    }
  },
  mounted() {
    this.callAPI(),
    this.checkSession()
  },
  methods: {
    listenInput(event) {
      const { value } = event.target
      this.search = value;
    },
    changeSession(s) {
      this.session = s
      this.session = localStorage.setItem('session', s)
    },
    changeUserId(id) {
      this.userId = id
      this.userId = localStorage.setItem('userId', id)
    },
    listenMenu(n) {
      this.menu = n
    },
    listenAccount() {
      this.account = !this.account
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
    },
    closeSession() {
      axios.delete(this.API_CLOSE + this.userId, { withCredentials: true })
        .then(response => {
          this.listenAccount()
          this.changeSession(false)
          this.changeUserId(false)
          localStorage.removeItem('userId')
          localStorage.removeItem('session')
        })
        .catch(error => {
        });
    },
    async checkSession() {     
      
      if (!!this.session === true) {
        const response = await fetch(this.API_LOGIN, { credentials: 'include' })
        if (response.status === 200) {
          this.listenAccount()
        }
      }
    }
  },
  beforeRouteLeave(to, from, next) {
    this.closeSession()
    next();
  }
}
</script>

<template>
  <Header v-if="loading" @listenInput="listenInput" :search="search" @listenMenu="listenMenu" :menu="menu"
    :account="account" @closeSession="closeSession" />
  <div v-if="loading" class="container-page">
    <Aside />
    <RouterView :search="this.search" :userId="this.userId"/>
  </div>
  <div v-else class="loading">
    <img class="loading__logo" src="/src/assets/img/logo.svg" alt="Imagen del logo" />
    <p class="loading__text">Se está conectando con el servidor</p>
  </div>
  <Login @listenMenu="listenMenu" :userId="userId" :menu="menu" :session="session" :account="account"
    @listenAccount="listenAccount" @changeSession="changeSession" @changeUserId="changeUserId" v-if="menu == 1" />
  <Signin @listenMenu="listenMenu" :menu="menu" v-if="menu == 2" />
  <div class="popup__bg" :class="{ popup__bg__active: menu }" @click="listenMenu(0)"></div>
</template>

