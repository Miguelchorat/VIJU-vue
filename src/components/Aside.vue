<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
    <aside class="aside">
        <nav class="aside__nav">
            <h2 v-if="!$route.path.includes('/perfil')" class="aside__nav__title">TEMAS</h2>
            <ul v-if="!$route.path.includes('/perfil')" class="aside__nav__list">
                <li class="aside__nav__list__item">                    
                    <RouterLink class="aside__nav__list__item__link" to="/">
                        <span class="aside__nav__list__item__icon material-symbols-outlined">home</span>
                        INICIO
                    </RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/perfil">PERFIL</RouterLink>
                </li>
                <li class="aside__nav__list__item">                    
                    <RouterLink class="aside__nav__list__item__link" to="/crear-review">
                        <span class="aside__nav__list__item__icon material-symbols-outlined">reviews</span>
                        CREAR REVIEW
                    </RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/review">REVIEW</RouterLink>
                </li>
            </ul>
            <h2 v-if="$route.path.includes('/perfil')" class="aside__nav__title">MI CUENTA</h2>
            <ul v-if="$route.path.includes('/perfil')" class="aside__nav__list">
                <li class="aside__nav__list__item">                    
                    <RouterLink class="aside__nav__list__item__link" to="/perfil">
                        <span class="aside__nav__list__item__icon material-symbols-outlined">person</span>
                        PERFIL
                    </RouterLink>
                </li>
                <li class="aside__nav__list__item">                    
                    <RouterLink class="aside__nav__list__item__link" to="/perfil/reviews">
                        <span class="aside__nav__list__item__icon material-symbols-outlined">reviews</span>
                        RESEÑAS
                    </RouterLink>
                </li>                
            </ul>
        </nav>
    </aside>
</template>