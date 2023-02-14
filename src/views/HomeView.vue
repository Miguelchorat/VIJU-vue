<script setup>
import Review from '../components/Review.vue'
</script>

<script>
export default {
  props: ["review","search"],
  data() {
    return {
      MAX_LENGHT: 85,
      results: null,
      API: "http://127.0.0.1:3001/api/v1/reviews",
      API_SEARCH: "http://127.0.0.1:3001/api/v1/reviews/search="+this.search
    }
  },
  mounted(){
    this.callAPI()
  },
  watch : {
    search: function() {
      this.API_SEARCH = "http://127.0.0.1:3001/api/v1/reviews/search="+this.search
      this.callAPI()
    }
  },
  methods: {
    async callAPI(){
      const endpoint = this.search !== "" ? this.API_SEARCH : this.API
      const response = await fetch(endpoint)
      const data = await response.json()
      this.results = data
    }    
  }
}
</script>

<template>
  <main class="main">    
    <h1 class="main__title">NUEVAS RESEÑAS</h1>
    <section class="main__reviews" v-if="this.results!=null && this.results.length !== 0">
      <Review v-for="res in this.results" :title='res.title' :image='res.image'
        :description='res.message.substring(0,MAX_LENGHT)+" ..."'
        :user='"Sleykun"' :score='res.score' @click="() => this.$emit('selectReview',res.id)"/>
    </section>
    <section v-else class="main__empty">
        <img src="/src/assets/img/broken.png" alt="CD ROTO" class="main__empty__image">
        <h2 className="main__empty__title">No se ha encontrado ningun resultado.</h2>
    </section>
  </main>
</template>
