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
            </ul>
        </nav>
    </aside>
</template>