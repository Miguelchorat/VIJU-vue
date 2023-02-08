<script setup>
import { RouterLink } from 'vue-router'
</script>

<script>
export default {
    props: ['menu','account'],
    data() {
        return {
            submenu: false,
        }
    },
    methods: {
        listenSubmenu() {
            this.submenu = !this.submenu
        },
    }
}
</script>

<template>
    <header class="header">
        <RouterLink to="/" class="header__identity">
            <img class="header__identity__logo" src="../assets/img/logo.svg" alt="Imagen del logo">
            <p class="header__identity__name">VIJU</p>
        </RouterLink>
        <div class="header__browser">
            <span class="header__browser__icon material-symbols-outlined">search</span>
            <input class="header__browser__input" placeholder="Buscar..."
                @input="(e) => this.$emit('listenInput', e)" />
        </div>
        <nav class="header__nav" v-if="!account">
            <ul class="header__nav__list">
                <li class="header__nav__list__item">
                    <a type="button" class="header__nav__list__item__link" href="#"
                        @click="() => this.$emit('listenMenu', 1)">LOG IN</a>
                </li>
                <li class="header__nav__list__item"><a type="button" class="header__nav__list__item__link" href="#"
                        @click="() => this.$emit('listenMenu', 2)">SIGN
                        IN</a></li>
            </ul>
        </nav>
        <a href="#" class="header__account" v-else @click="listenSubmenu">
            @Sleykun
            <nav class="header__menu" v-if="this.submenu">
                <ul class="header__menu__list">
                    <li class="header__menu__list__item"><RouterLink to="/perfil">PERFIL</RouterLink></li>
                    <li class="header__menu__list__item"><RouterLink to="/crear-reseña">CREAR REVIEW</RouterLink></li>
                    <li class="header__menu__list__item" @click="() => this.$emit('listenAccount')">CERRAR SESIÓN</li>
                </ul>
                <span class="header__menu__square" />
            </nav>
        </a>
        
        <!-- <a class="header__menu--disabled" href="#">
            <span class="header__menu__icon material-symbols-outlined">menu</span>
        </a> -->
    </header>
</template>
