<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
    <aside class="aside">
        <nav class="aside__nav">
            <ul v-if="!$route.path.includes('/perfil')" class="aside__nav__list">
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/">INICIO</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/nuevos">NUEVOS</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/perfil">PERFIL</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/crear-review">CREAR REVIEW</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/review">REVIEW</RouterLink>
                </li>
            </ul>
            <ul v-else class="aside__nav__list">
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/perfil">MI PERFIL</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/perfil/reviews">MIS RESEÑAS</RouterLink>
                </li>                
            </ul>
        </nav>
    </aside>
</template>