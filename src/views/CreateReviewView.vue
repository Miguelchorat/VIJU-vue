<script>
export default {
    data() {
        return {
            games: null,
            API_GAMES: "http://localhost:3001/api/v1/games"
        }
    },
    methods: {
        async callAPIGames() {
            const response = await fetch(this.API_GAMES)
            const data = await response.json()
            this.games = data
        }
    }
}
</script>

<template>
    <main class="main">
        <h1 class="main__title">CREAR RESEÑA</h1>
        <form class="main__form">
            <div class="main__form__group">
                <div class="main__form__field">
                    <input class="main__form__field__input" type="text" placeholder="Título" aria-label="title"
                        required />
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">El título no es válido</p>
                </div>

                <div class="main__form__field">
                    <select class="main__form__field__select" name="videogames" @click="callAPIGames">
                        <option value="default" selected>VIDEOJUEGOS</option>
                        <option value="-----">- - - - -</option>
                        <option v-for="d in this.games" :value="d.name">{{d.name}}</option>
                    </select>
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">La puntuación no es válida</p>
                </div>

                <div class="main__form__field">
                    <input class="main__form__field__input" type="number" placeholder="Puntuación" aria-label="score"
                        required />
                    <span class="main__form__field__square" />
                    <p class="main__form__field__error">La puntuación no es válida</p>
                </div>
            </div>
            <div class="main__form__field">
                <textarea class="main__form__field__textarea" type="text" placeholder="Texto" aria-label="text"
                    required />
                <span class="main__form__field__square" />
                <p class="main__form__field__error">El título no es válido</p>
            </div>
            <input class="main__form__button" type="button" value="CREAR RESEÑA">
        </form>
    </main>
</template>