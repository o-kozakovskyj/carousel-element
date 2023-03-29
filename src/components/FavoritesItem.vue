<template>
  <li
    class="list-group-item d-flex justify-content-between align-items-center list-item"
  >
    <div>
      <span
        id="boot-icon"
        :class="{
          'bi-star-fill icon': favorites.isFavorite,
          'bi-star icon': !favorites.isFavorite,
        }"
        style="font-size: 1rem; color: #ffc107"
        @click.stop="removeFromFavoriteList(favorites.id)"
      ></span>
      {{ favorites.author }}
    </div>

    <div class="image-parent">
      <img
        :src="favorites.download_url"
        :alt="favorites.author"
        class="image"
      />
    </div>
  </li>
</template>
<script>
export default {
  props: {
    favorites: {
      type: Object,
      required: true,
    },
  },
  methods: {
    removeFromFavoriteList(id) {
      this.$emit("removeFromFavoriteList", id);
    },
  },
};
</script>
