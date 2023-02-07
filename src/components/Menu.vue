<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
    <aside class="aside">
        <nav class="aside__nav">
            <ul class="aside__nav__list">
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
                    <RouterLink class="aside__nav__list__item__link" to="/crear-reseña">CREAR REVIEW</RouterLink>
                </li>
                <li class="aside__nav__list__item">
                    <RouterLink class="aside__nav__list__item__link" to="/reseña">REVIEW</RouterLink>
                </li>
            </ul>
        </nav>
    </aside>
</template>