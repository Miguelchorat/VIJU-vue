<script>
export default {
  props: ["review"],
  data() {
    return {
      results: null,
      API_REVIEW: "http://127.0.0.1:3001/api/v1/reviews/"+this.review
    }
  },
  mounted(){
    this.callAPI()
  },
  methods: {
    async callAPI(){
      const response = await fetch(this.API_REVIEW)
      const data = await response.json()
      this.results = data
    }    
  }
}
</script>

<template>
    <main v-if="results" class="main main--review">
        <header class="main__header main__header--review">
            <h2 class="main__header__title">{{results.name}}</h2>
            <div class="main__header__background">
                <img className="main__header__background__img" :src="results.image  "/>     
                <div className="main__header__background__opacity" />
            </div>            
            <p class="main__header__score" :class="results.score < 2.5 ? 'main__header__score__red' : (results.score >= 2.5 && results.score < 3.5) ? 'main__header__score__yellow' : 'main__header__score__green'">{{results.score}}</p>
            <p class="main__header__date">Creado por {{results.username}} el {{results.created_at}}</p>
        </header>
        <section class="main__review">
            <h3 class="main__review__title">{{results.title}}</h3>
            <p class="main__review__description">{{ results.message }}</p>
        </section>
    </main>
</template>