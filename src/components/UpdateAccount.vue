<script>
export default {
    props: ['menu'],

    data() {
        return {
            email: 'PLACEHOLDER@gmail.com',
            password: '',
            repeatPassword: '',
            username: 'PLACEHOLDER',
            date: '1996-09-29',
            errorEmail: false,
            errorPassword: false,
            errorRepeatPassword: false,
            errorUsername: false,
            errorDate: false,
            remember: false,
            visibility: false,
            emailValidation: /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/,
            passwordValidation: /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,32}$/,
            usernameValidation: /^[a-zA-Z]{3,18}$/,
            MIN_AGE_LIMIT: new Date(Date.now()).getFullYear()-13,
            MAX_AGE_LIMIT: new Date(Date.now()).getFullYear()+120
        }
    },
    methods: {
        listenRemember() {
            this.remember = !this.remember
        },
        listenVisibility() {
            this.visibility = !this.visibility
        },
        checkFields(){
            let check = 0
            this.errorEmail = false
            this.errorPassword = false
            this.errorRepeatPassword = false
            this.errorDate = false
            this.errorUsername = false

            if(this.emailValidation.test(this.email)){
                check++
            } else{
                this.errorEmail = true
            }

            if(this.usernameValidation.test(this.username)){
                check++   
            } else {
                this.errorUsername = true
            }

            if(this.passwordValidation.test(this.password)){
                check++   
            } else {
                this.errorPassword = true
            }

            if(this.repeatPassword !== "" && this.repeatPassword === this.password){
                check++   
            } else {
                this.errorRepeatPassword = true
            }

            if(this.date!=='' && (new Date(this.date).getFullYear() < this.MIN_AGE_LIMIT || new Date(this.date).getFullYear() > this.MAX_AGE_LIMIT)){
                check++   
            } else {
                this.errorDate = true
            }

            if(check == 5){
                this.$emit('listenMenu')
            }
        }
    }
}
</script>

<template>
    <form class="session session--update" :class="{ session__active: menu }">
        <a class="session__close material-symbols-outlined" href="#" @click="() => this.$emit('listenMenu')">close</a>
        <h2 class="session__title">MODIFICAR</h2>
        <div class="session__field">
            <input class="session__field__input" type="text" :value="username" @input="event => username = event.target.value"
                placeholder="Nombre de usuario" aria-label="username" :class="{ session__field__input__warning: errorUsername }"/>
            <span class="session__field__square" :class="{ session__field__square__active: errorUsername }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorUsername }">Nombre de usuario no válido</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorEmail }" type="email"
                placeholder="Correo" aria-label="email" required :value="email" @input="event => email = event.target.value"/>
            <span class="session__field__square" :class="{ session__field__square__active: errorEmail }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorEmail }">El correo no es válido</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorPassword }" :value="password" @input="event => password = event.target.value"
                placeholder="Clave" :type="visibility ? 'text' : 'password'" aria-label="password" required maxlength="32"/>
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{this.visibility ? 'visibility_off' : 'visibility'}}</span>
            <span class="session__field__square" :class="{ session__field__square__active: errorPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorPassword }">La contraseña no es
                válida</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" :class="{ session__field__input__warning: errorRepeatPassword }" :value="repeatPassword" @input="event => repeatPassword = event.target.value"
                placeholder="Repetir clave" :type="visibility ? 'text' : 'password'" aria-label="repeat-password" required maxlength="32"/>
            <span class="session__field__icon material-symbols-outlined" @click="listenVisibility">{{this.visibility ? 'visibility_off' : 'visibility'}}</span>
            <span class="session__field__square" :class="{ session__field__square__active: errorRepeatPassword }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorRepeatPassword }">Las contraseñas no son iguales</p>
        </div>
        <div class="session__field">
            <input class="session__field__input" type="date" :class="{ session__field__input__warning: errorDate }" aria-label="date" :value="this.date" @input="event => this.date = event.target.value"/>            
            <span class="session__field__square" :class="{ session__field__square__active: errorDate }" />
            <p class="session__field__error" :class="{ session__field__error__active: errorDate }">La fecha no es válida</p>
        </div>
        <input class="session__button" type="button" @click="checkFields" value="MODIFICAR">
    </form>
</template>