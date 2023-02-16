<script>
import axios from 'axios'

export default {
    props: ['menu'],

    data() {
        return {
            email: '',
            password: '',
            repeatPassword: '',
            username: '',
            date: '',
            errorEmail: '',
            errorPassword: '',
            errorRepeatPassword: '',
            errorUsername: '',
            errorDate: '',
            remember: '',
            focusUsername: false,
            focusEmail: false,
            focusPassword: false,
            focusRepeatPassword: false,
            focusDate: false,
            visibility: false,
            visibilityRepeat: false,
            API_REGISTER: "http://127.0.0.1:3001/api/v1/users/",
            emailValidation: /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/,
            passwordValidation: /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,32}$/,
            usernameValidation: /^[a-zA-Z]{3,18}$/,
            MIN_AGE_LIMIT: new Date(Date.now()).getFullYear() - 13,
            MAX_AGE_LIMIT: new Date(Date.now()).getFullYear() + 120
        }
    },
    methods: {
        listenRemember() {
            this.remember = !this.remember
        },
        listenVisibility() {
            this.visibility = !this.visibility
        },
        listenVisibilityRepeat() {
            this.visibilityRepeat = !this.visibilityRepeat
        },
        async registerAccount() {
            const encoder = new TextEncoder();
            const data = encoder.encode(this.password);
            const digest = await crypto.subtle.digest('SHA-1', data);
            const hash = Array.from(new Uint8Array(digest)).map(b => b.toString(16).padStart(2, '0')).join('');

            await axios.post(this.API_REGISTER, {
                username: this.username,
                email: this.email,
                date: this.date,
                password: hash
            }, {
                headers: {
                    'Content-Type': 'application/json'
                }
            })
                .then(response => {
                    if (response.data.success) {
                        this.$emit('listenMenu', 1)
                    }
                    if (response.data.errorEmail) {
                        this.errorEmail = 'El correo ya está registrado'
                    }
                    if (response.data.errorUsername) {
                        this.errorUsername = 'El nombre de usuario ya está registrado'
                    }
                })
                .catch(error => {
                    console.error("Fallo al enviar el form" + error)
                });
        },
        checkFields() {
            let check = 0
            this.errorEmail = ''
            this.errorPassword = ''
            this.errorRepeatPassword = ''
            this.errorDate = ''
            this.errorUsername = ''

            if (this.emailValidation.test(this.email)) {
                check++
            } else {
                this.errorEmail = 'El correo no es válido'
            }

            if (this.usernameValidation.test(this.username)) {
                check++
            } else {
                this.errorUsername = 'Nombre de usuario no válido'
            }

            if (this.passwordValidation.test(this.password)) {
                check++
            } else {
                this.errorPassword = 'La contraseña no es válida. Debe contener al menos 8 caracteres y un número.'
            }

            if (this.repeatPassword !== "" && this.repeatPassword === this.password) {
                check++
            } else {
                this.errorRepeatPassword = 'Las contraseñas no son iguales'
            }
            if (this.date !== '' && (new Date(this.date).getFullYear() < this.MIN_AGE_LIMIT || new Date(this.date).getFullYear() > this.MAX_AGE_LIMIT)) {
                check++
            } else {
                this.errorDate = 'La fecha no es válida'
            }

            if (check == 5) {
                this.registerAccount()
            }
        }
    }
}
</script>

<template>
    <form class="session session--signin" @submit.prevent="checkFields">
        <a class="session__close material-symbols-outlined" href="#" @click="() => this.$emit('listenMenu')">close</a>
        <h2 class="session__title">REGISTRARSE</h2>
        <div class="session__field">
            <input class="session__field__input" type="text" :value="username"
                @input="event => username = event.target.value" placeholder="Nombre de usuario" aria-label="username"
                :class="{ session__field__input__warning: errorUsername }" @focus="focusUsername = true"
                @blur="focusUsername = false" />
            <span class="session__field__square"
                :class="{ session__field__square__active: errorUsername && focusUsername }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorUsername && focusUsername }">
                {{ errorUsername }}</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorEmail }" type="email"
                placeholder="Correo" aria-label="email" :value="email" @input="event => email = event.target.value"
                @focus="focusEmail = true" @blur="focusEmail = false" />
            <span class="session__field__square"
                :class="{ session__field__square__active: errorEmail && focusEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorEmail && focusEmail }">{{
                errorEmail
            }}</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorPassword }"
                :value="password" @input="event => password = event.target.value" placeholder="Clave"
                :type="visibility ? 'text' : 'password'" aria-label="password" maxlength="32"
                @focus="focusPassword = true" @blur="focusPassword = false" />
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{
                this.visibility ?
                    'visibility_off' : 'visibility'
            }}</span>
            <span class="session__field__square"
                :class="{ session__field__square__active: errorPassword && focusPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorPassword && focusPassword }">
                {{ errorPassword }}</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorRepeatPassword }"
                :value="repeatPassword" @input="event => repeatPassword = event.target.value"
                placeholder="Repetir clave" :type="visibilityRepeat ? 'text' : 'password'" aria-label="repeat-password"
                maxlength="32" @focus="focusRepeatPassword = true" @blur="focusRepeatPassword = false" />
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibilityRepeat">{{
                this.visibilityRepeat ? 'visibility_off' : 'visibility'
            }}</span>
            <span class="session__field__square"
                :class="{ session__field__square__active: errorRepeatPassword && focusRepeatPassword }" />
            <p class="session__field__error"
                :class="{ session__field__error__active: errorRepeatPassword && focusRepeatPassword }">{{
                    errorRepeatPassword
                }}</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" type="date" :class="{ session__field__input__warning: errorDate }"
                aria-label="date" :value="this.date" @input="event => this.date = event.target.value"
                @focus="focusDate = true" @blur="focusDate = false" />
            <span class="session__field__square" :class="{ session__field__square__active: errorDate && focusDate }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorDate && focusDate }">{{
                errorDate
            }}</p>
        </div>
        <input class="session__button" type="submit" value="REGISTRARSE">
        <div class="session__signin">
            <label class="session__signin__label">¿Ya tienes una cuenta?</label>
            <a href="#" class="session__signin__link" @click="() => this.$emit('listenMenu', 1)"
                @mousedown="cleanFields">Iniciar sesión</a>
        </div>
    </form>
</template>