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
    <form class="login" :class="{ login__active: menu }">
        <a class="login__close material-symbols-outlined" href="#" @click="() => this.$emit('listenMenu')">close</a>
        <h2 class="login__title">INICIAR SESIÓN</h2>
        <div class="login__field">
            <input class="login__field__input" :class="{ login__field__input__warning: errorEmail }" type="email"
                placeholder="Email" aria-label="email" required />
            <span class="login__field__square" :class="{ login__field__square__active: errorEmail }" />
            <p class="login__field__error" :class="{ login__field__error__active: errorEmail }">El correo no es válido</p>
        </div>
        <div class="login__field">
            <input class="login__field__input" :class="{ login__field__input__warning: errorPassword }" 
                placeholder="Password" :type="visibility ? 'text' : 'password'" aria-label="password" required maxlength="32"/>
            <span class="login__field__icon material-symbols-outlined" @click="listenVisibility">{{this.visibility ? 'visibility_off' : 'visibility'}}</span>
            <span class="login__field__square" :class="{ login__field__square__active: errorPassword }" />
            <p class="login__field__error" :class="{ login__field__error__active: errorPassword }">La contraseña no es
                válida</p>
        </div>
        <div class='login__remember'>
            <input type="checkbox" :checked="remember" @click="listenRemember"
                class="login__remember__checkbox"/>
            <label class="login__remember__label">Recordarme</label>
        </div>
        <button class="login__button" type="submit">INICIAR SESIÓN</button>
        <div class="login__signin">
            <label class="login__signin__label">¿No tienes cuenta?</label>
            <a href="#" class="login__signin__link">Create una</a>
        </div>
    </form>
</template>