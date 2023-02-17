<script>
export default {
    data() {
        return {
            title: '',
            message: '',
            score: '',
            videogame: '',
            errorTitle: false,
            errorMessage: false,
            errorScore: false,
            errorVideogame: false,
            games: null,
            API_GAMES: "http://localhost:3001/api/v1/games",
            API_CREATE_REVIEW: "http://localhost:3001/api/v1/reviews",
            scoreValidation: /^(?:[0-5](?:\.[0-9])?|\.[0-9])$/,
        }
    },
    methods: {
        async callAPIGames() {
            const response = await fetch(this.API_GAMES)
            const data = await response.json()
            this.games = data
        }
    },
    async createReview() {
        const response = await axios.post(this.API_CREATE_REVIEW, {
            title: this.title,
            message: this.message,
            videogame: this.videogame,
            score: this.score,
            user: 1
        }, { withCredentials: true })

        if (response.status === 200) {

        }
    },
    checkFields() {
        let check = 0
        this.errorTitle = false
        this.errorMessage = false
        this.errorScore = false
        this.errorVideogame = false

        if (this.title.length<3 || this.title.length>50) {
            check++
        } else {
            this.errorTitle = true
        }

        if (this.message.length<3) {
            check++
        } else {
            this.errorMessage = true
        }

        if (this.scoreValidation.test(this.score)) {
            check++
        } else {
            this.errorScore = true
        }

        if (check == 2) {
            this.loginAccount()
        }
    }
}
</script>

<template>
    <main class="main">
        <h1 class="main__title">CREAR RESEÑA</h1>        
        <!-- <div class="main__background">
            <img className="main__background__img" src="/src/assets/img/background.png" />
            <div className="main__background__opacity" />
        </div> -->
        <form class="main__form" @submit.prevent="callApi">
            <div class="main__form__group">
                <div class="main__form__field">
                    <input class="main__form__field__input" type="text" placeholder="Título" aria-label="title" required
                        :value="title" @input="event => title = event.target.value" maxlength="50"/>
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">El título no es válido</p>
                </div>

                <div class="main__form__field">
                    <select class="main__form__field__select" name="videogames" @click="callAPIGames">
                        <option value="default" selected>VIDEOJUEGOS</option>
                        <option value="-----">- - - - -</option>
                        <option v-for="d in this.games" :value="d.name">{{ d.name }}</option>
                    </select>
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">La puntuación no es válida</p>
                </div>

                <div class="main__form__field">
                    <input class="main__form__field__input" type="number" placeholder="Nota" aria-label="score" required
                        :value="score" @input="event => score = event.target.value" />
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">La puntuación no es válida</p>
                </div>
            </div>
            <div class="main__form__field">
                <textarea class="main__form__field__textarea" type="text" placeholder="Texto" aria-label="text" required
                    :value="message" @input="event => message = event.target.value" />
                <span class="main__form__field__square" />
                <p class="main__form__field__error">El título no es válido</p>
            </div>
            <input class="main__form__button" type="submit" value="CREAR RESEÑA">
        </form>        
    </main>
</template>