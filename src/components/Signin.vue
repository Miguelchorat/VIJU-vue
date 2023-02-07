<script>
export default {
    props: ['menu'],

    data() {
        return {
            errorEmail: false,
            errorPassword: false,
            remember: false,
            visibility: false
        }
    },
    methods: {
        listenRemember() {
            this.remember = !this.remember
        },
        listenVisibility() {
            this.visibility = !this.visibility
        }
    }
}
</script>

<template>
    <form class="session session--signin" :class="{ session__active: menu == 2 }">
        <a class="session__close material-symbols-outlined" href="#" @click="() => this.$emit('listenMenu')">close</a>
        <h2 class="session__title">REGISTRARSE</h2>
        <div class="session__field">
            <input class="session__field__input" type="text"
                placeholder="Nombre de usuario" aria-label="username" :class="{ session__field__input__warning: errorEmail }" required />
            <span class="session__field__square" :class="{ session__field__square__active: errorEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorEmail }">Nombre de usuario no válido</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorEmail }" type="email"
                placeholder="Correo" aria-label="email" required />
            <span class="session__field__square" :class="{ session__field__square__active: errorEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorEmail }">El correo no es válido</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorPassword }" 
                placeholder="Clave" :type="visibility ? 'text' : 'password'" aria-label="password" required maxlength="32"/>
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{this.visibility ? 'visibility_off' : 'visibility'}}</span>
            <span class="session__field__square" :class="{ session__field__square__active: errorPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorPassword }">La contraseña no es
                válida</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorPassword }" 
                placeholder="Repetir clave" :type="visibility ? 'text' : 'password'" aria-label="repeat-password" required maxlength="32"/>
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{this.visibility ? 'visibility_off' : 'visibility'}}</span>
            <span class="session__field__square" :class="{ session__field__square__active: errorRepeatPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorRepeatPassword }">Las contraseñas no son iguales</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" type="date" aria-label="date"/>            
            <span class="session__field__square" :class="{ session__field__square__active: errorDate }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorDate }">La fecha no es válida</p>
        </div>
        <button class="session__button" type="submit">INICIAR SESIÓN</button>
        <div class="session__signin">
            <label class="session__signin__label">¿Ya tienes una cuenta?</label>
            <a href="#" class="session__signin__link" @click="() => this.$emit('listenMenu', 1)">Iniciar sesión</a>
        </div>
    </form>
</template>