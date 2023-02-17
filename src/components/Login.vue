<script>
import axios from 'axios'

export default {
    props: ['menu', 'account', 'session', 'userId'],

    data() {
        return {
            email: '',
            password: '',
            errorEmail: '',
            errorPassword: '',
            errorSession: '',
            remember: false,
            visibility: false,
            focusEmail: false,
            focusPassword: false,
            API_LOGIN: "http://127.0.0.1:3001/api/v1/auth/users/",
            emailValidation: /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/,
            passwordValidation: /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,32}$/
        }
    },
    methods: {
        listenRemember() {
            this.remember = !this.remember
        },
        listenVisibility() {
            this.visibility = !this.visibility
        },
        async loginAccount() {
            const encoder = new TextEncoder();
            const data = encoder.encode(this.password);
            const digest = await crypto.subtle.digest('SHA-1', data);
            const hash = Array.from(new Uint8Array(digest)).map(b => b.toString(16).padStart(2, '0')).join('');

            await axios.post(this.API_LOGIN, {
                email: this.email,
                password: hash
            }, { withCredentials: true })
            .then(response => {
                if (this.remember){
                    this.$emit('changeSession', true)   
                    this.$emit('changeUserId', response.data) 
                }                                      
                this.$emit('listenAccount')
                this.$emit('listenMenu', 0)
            })
            .catch(error => {
                if (error.response.status === 401) {
                    this.errorSession = 'El correo o contraseña no es correcta'
                }
            })
        },
        checkFields() {
            let check = 0
            this.errorEmail = ''
            this.errorPassword = ''
            this.errorSesion = ''

            if (this.emailValidation.test(this.email)) {
                check++
            } else {
                this.errorEmail = 'El correo no es válido'
            }

            if (this.passwordValidation.test(this.password)) {
                check++
            } else {
                this.errorPassword = 'La contraseña no es válida. Debe contener al menos 8 caracteres y un número.'
            }

            if (check == 2) {
                this.loginAccount()
            }
        }
    }
}
</script>
<template>
    <form class="session" @submit.prevent="checkFields">
        <a class="session__close material-symbols-outlined" href="#" @click="() => this.$emit('listenMenu')">close</a>
        <h2 class="session__title">INICIAR SESIÓN</h2>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorEmail || errorSession }" type="email"
                placeholder="Correo" aria-label="email" :value="email" @input="event => email = event.target.value"
                @focus="focusEmail = true" @blur="focusEmail = false" />
            <span class="session__field__square" :class="{ session__field__square__active: errorEmail && focusEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorEmail && focusEmail }">{{
                errorEmail
            }}</p>
            <span class="session__field__square" :class="{ session__field__square__active: errorSession && focusEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorSession && focusEmail }">{{
                errorSession
            }}</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorPassword }"
                :value="password" @input="event => password = event.target.value" placeholder="Clave"
                :type="visibility ? 'text' : 'password'" aria-label="password" maxlength="20" 
                @focus="focusPassword = true" @blur="focusPassword = false"/>
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{
                this.visibility ?
                'visibility_off' : 'visibility'
            }}</span>
            <span class="session__field__square"
                :class="{ session__field__square__active: errorPassword && focusPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorPassword && focusPassword }">
                {{ errorPassword }}</p>
        </div>
        <div class='session__remember'>
            <input type="checkbox" :checked="remember" @click="listenRemember" class="session__remember__checkbox" />
            <label class="session__remember__label">Recordarme</label>
        </div>
        <input class="session__button" type="submit" value="INICIAR SESIÓN">
        <div class="session__signin">
            <label class="session__signin__label">¿No tienes cuenta?</label>
            <a href="#" class="session__signin__link" @click="() => this.$emit('listenMenu', 2)">Create una</a>
        </div>
    </form>
</template>