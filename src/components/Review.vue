<script>
import { RouterLink } from 'vue-router';

export default {
    props: ["title", "image", "description", "user", "score"]
}
</script>

<template>
    <RouterLink href="#" class="main__reviews__review" to="/review">
        <img class="main__reviews__review__img" :src="this.image" alt="" />
        <h2 class="main__reviews__review__title">{{ this.title }}</h2>
        <p class="main__reviews__review__description">{{ this.description }}</p>
        <div class="main__reviews__review__info">
            <p class="main__reviews__review__info__user">@{{ this.user }}</p>
            <p class="main__reviews__review__info__score"
                :class="this.score < 2.5 ? 'main__reviews__review__info__score__red' : (this.score >= 2.5 && this.score < 3.5) ? 'main__reviews__review__info__score__yellow' : 'main__reviews__review__info__score__green'">
                {{ this.score }}
            </p>
        </div>
    </RouterLink>
</template>

