<template>
  <div class="py-5 row gy-3 justify-content-around">
    <div
      v-for="photo in photos"
      :key="photo.id"
      class="col-12 col-sm-6 col-md-4 d-flex justify-content-center"
    >
      <img
        @click="$emit('changePhotoIndex', photo.id)"
        class="rounded"
        :src="photo.src.small"
        alt=""
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Thumbnails-Component",
  props: {
    photos: Array,
  },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
img {
  cursor: pointer;
}
</style>
