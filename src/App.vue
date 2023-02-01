<script setup>
import { RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Menu from './components/Menu.vue'
</script>

<script>
  export default {
    data() {
      return {
        search: ""
      }
    },
    methods: {
      handleChange(event){
        const {value} = event.target
        this.search = value;
      }
    }
  }
</script>

<template>
  <Header @inputChange="handleChange" :search="search"/>
  <div class="container-page">
    <Menu />
    <RouterView />
  </div>
</template>

