<script setup>
import UpdateAccount from '../components/UpdateAccount.vue'
</script>

<script>
export default {
  data() {
    return {
      menu: false      
    }
  },
  methods: {
    listenMenu() {
      this.menu = !this.menu
    }
  }
}
</script>

<template>
    <main class="main">    
        <header class="main__header">
            <h2 class="main__header__title">MI CUENTA</h2>
        </header>
        <section class="main__profile">
            <h3 class="main__profile__title">NOMBRE DE USUARIO</h3>
            <p class="main__profile__text">Sleykun</p>
            <h3 class="main__profile__title">CORREO</h3> 
            <p class="main__profile__text">PLACEHOLDER@correo.com</p>
            <h3 class="main__profile__title">FECHA DE NACIMIENTO</h3>
            <p class="main__profile__text">01/01/1970</p>  
            <input type='button' class="main__profile__button" value="MODIFICAR" @click="listenMenu"/>
        </section>            
    </main>       

    <UpdateAccount @listenMenu="listenMenu" :menu="menu" />
    <div class="popup__bg" :class="{ popup__bg__active: menu }" @click="listenMenu"></div>
</template>