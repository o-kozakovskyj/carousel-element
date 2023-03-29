<template>
  <div class="home">
    <carousel-page :carouselSlides="carouselSlides" />
  </div>
</template>
<script>
import CarouselPage from "./CarouselPage.vue";
export default {
  components: {
    CarouselPage,
  },
  data: () => ({
    carouselSlides: [],
  }),
  methods: {
    getSlidesFromAPI() {
      fetch("https://picsum.photos/v2/list?page=2&limit=10")
        .then((response) => response.json())
        .then((data) => {
          this.addIsFavoritePropertyToSlides(data);
          this.carouselSlides = data;
        });
    },
    addIsFavoritePropertyToSlides(slides) {
      slides.forEach((slide) => {
        slide.isFavorite = false;
      });
    },
  },
  created() {
    this.getSlidesFromAPI();
  },
};
</script>
