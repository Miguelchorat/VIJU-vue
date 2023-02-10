<script setup>
import Review from '../components/Review.vue'

defineProps({
  results: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <main class="main">
    <h1 class="main__title">TENDENCIAS</h1>
    <div v-for="res in this.results">
      <p>{{ res.title }}</p>
    </div>
    <div class="main__reviews">
      <Review v-for="n in 10" :title='"Esto es un titulo"' :img='"/src/assets/img/placeholder.png"'
        :description='"Esto es una descripción de prueba que va a ser bastante larga mantener la review..."'
        :user='"Sleykun"' :score='"3.5"' />
    </div>
  </main>
</template>
