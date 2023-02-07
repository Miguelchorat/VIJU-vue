<script>
export default {
    props: ['title','img','description','user','score'],
}
</script>

<template>
    <span href="#" class="main__reviews__review">
        <img class="main__reviews__review__img" :src="this.img" alt="" />
        <h2 class="main__reviews__review__title">{{ this.title }}</h2>
        <p class="main__reviews__review__description">{{ this.description }}</p>
        <div class="main__reviews__review__info">
            <p class="main__reviews__review__info__user">@{{ this.user }}</p>
            <p class="main__reviews__review__info__score">{{ this.score }}</p>
        </div>
    </span>
</template>