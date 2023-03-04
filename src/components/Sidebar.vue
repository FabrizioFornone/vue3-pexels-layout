<template>
  <nav class="sidebar bg-secondary">
    <div class="py-5 fs-6 d-flex flex-column">
      <button
        v-for="photo in photos"
        :key="photo.id"
        class="btn btn-light flex-fill m-2"
      >
        <div @click="$emit('changePhoto', photo.id)">
          {{ stringTruncate(photo.alt, 25) }}
        </div>
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Sidebar-Component",
  props: {
    photos: Array,
  },
  setup() {
    const stringTruncate = (string, char) => {
      if (string.length > char) {
        return string.slice(0, char) + "...";
      } else {
        return string;
      }
    };

    return { stringTruncate };
  },
};
</script>

<style lang="scss" scoped>
.sidebar {
  width: 300px;
}
</style>
