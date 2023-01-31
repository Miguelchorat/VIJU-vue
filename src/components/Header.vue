<script setup>
    // defineProps({
    //     search: {
    //         type: String,
    //         required: false
    //     }
    // })
</script>

<template>
    <header class="header">
        <a href="#" class="header__identity">
            <img class="header__identity__logo" src="./assets/img/logo.svg" alt="Imagen del logo">
            <p class="header__identity__name">VIJU</p>
        </a>        
        <form class="header__browser">
            <span class="header__browser__icon material-symbols-outlined">search</span>
            <input class="header__browser__input" placeholder="Buscar..." :value="search"/>                                            
        </form>
        <nav class="header__nav">
            <ul class="header__nav__list">
                <li class="header__nav__list__item"><a href="#">LOG IN</a></li>
                <li class="header__nav__list__item"><a href="#">SIGN IN</a></li>
            </ul>
        </nav>
        <a class="header__menu--disabled" href="#">
            <span class="header__menu__icon material-symbols-outlined">menu</span>
        </a>
    </header>
</template>
