<template class="carousel-page">
  <Carousel :settings="settings" :breakpoints="breakpoints" :wrap-around="true">
    <Slide v-for="slide in carouselSlides" :key="slide.id">
      <CarouselItem :slide="slide" @addToFavorites="changeFavoriteStatus" />
    </Slide>
    <template #addons>
      <Pagination :style="{ opacity: 0.5, color: 'white' }" />
      <Navigation />
    </template>
  </Carousel>
  <div class="container" v-show="favoriteList.length > 0">
    <div class="row">
      <div class="col-12 col-sm-8 col-lg-5">
        <h6 class="text-muted">My Favorites Pictures</h6>
        <transition-group name="list" tag="ul">
          <ul
            class="list-group"
            v-for="favorites in favoriteList"
            :key="favorites.id"
          >
            <FavoritesItem
              :favorites="favorites"
              @removeFromFavoriteList="changeFavoriteStatus"
            />
          </ul>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
import { Carousel, Navigation, Pagination, Slide } from "vue3-carousel";
import "vue3-carousel/dist/carousel.css";
import CarouselItem from "./CarouselItem.vue";
import FavoritesItem from "./FavoritesItem.vue";
export default {
  components: {
    Carousel,
    Slide,
    Navigation,
    CarouselItem,
    FavoritesItem,
    Pagination,
  },
  props: {
    carouselSlides: {
      type: Array,
      required: true,
    },
  },
  computed: {
    favoriteList() {
      return this.carouselSlides.filter((item) => item.isFavorite);
    },
  },
  methods: {
    changeFavoriteStatus(id) {
      this.carouselSlides.find((item) => item.id === id).isFavorite =
        !this.carouselSlides.find((item) => item.id === id).isFavorite;
    },
  },
  data: () => ({
    settings: {
      itemsToShow: 1,
      snapAlign: "center",
      transition: 500,
      mouseDrag: true,
      autoplay: 2000,
      pauseAutoplayOnHover: true,
    },
    isFavorite: false,
    breakpoints: {
      700: {
        itemsToShow: 3.5,
        snapAlign: "center",
      },
      1024: {
        itemsToShow: 5,
        snapAlign: "start",
      },
    },
  }),
};
</script>
<style lang="scss">
.carousel-page {
  display: flex;
  align-items: center;
  justify-content: center;
  .carousel {
    margin: 0 auto;
    max-width: 100%;
    padding: 0 1rem;
    .carousel__inner-slide {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
    }
  }
}
.container {
  max-width: 100%;
  margin-top: 2rem;
}
.row {
  margin-top: 4rem;
  justify-content: center;
}
.carousel__item {
  margin: 0 1rem;
}
.icon {
  margin: 0.5rem;
}
.carousel__item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.image-parent {
  width: 50px;
  height: 50px;
  overflow: hidden;
  border-radius: 10%;
  margin-left: 1rem;
}
.image-parent img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.list-group {
  margin-top: 1rem;
  &-item {
    border: none;
    border-radius: 0;
    padding: 0.5rem 0;
    &:nth-child(odd) {
      background-color: #f8f9fa;
    }
  }
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.slide-leave-active,
.slide-enter-active {
  transition: opacity 0.5s;
}
.slide-enter {
  transform: translate(100%, 0);
  opacity: 0;
}
.slide-leave-to {
  transform: translate(-100%, 0);
  opacity: 0;
}
</style>
