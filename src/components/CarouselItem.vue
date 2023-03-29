<template>
  <div class="card carousel__item" style="width: 18rem">
    <img class="card-img-top" :src="slide.download_url" :alt="slide.author" />
    <div class="card-body">
      <p class="card-text">{{ slide.author }}</p>
      <span
        id="boot-icon"
        :class="{
          'bi-star-fill': slide.isFavorite,
          'bi-star': !slide.isFavorite,
        }"
        style="font-size: 1rem; color: #ffc107"
        @click="$emit('addToFavorites', slide.id)"
      ></span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    slide: {
      type: Object,
      required: true,
    },
  },
};
</script>
