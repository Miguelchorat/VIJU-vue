<script setup>
  import { RouterLink } from 'vue-router'
</script>

<template>
    <aside class="aside">
        <nav class="aside__nav">
            <ul class="aside__nav__list">
                <li class="aside__nav__list__item"><RouterLink to="/">Inicio</RouterLink></li>
                <li class="aside__nav__list__item"><RouterLink to="/nuevos">Nuevos</RouterLink></li>
            </ul>
        </nav>
    </aside> 
</template>