<template>
  <main class="container bg-secondary">
    <div v-if="getSelectedPhoto()">
      <div class="d-flex justify-content-center text-white">
        <h5>{{ getSelectedPhoto().photographer }}</h5>
        <a :href="getSelectedPhoto().photographer_url" class="ms-2"
          >author link</a
        >
      </div>
      <div class="main-photo d-flex justify-content-center">
        <img class="img-fluid" :src="getSelectedPhoto().src.landscape" alt="" />
      </div>
    </div>
    <thumbnails
      @changePhotoIndex="changePhotoIndex"
      :photos="photos"
    ></thumbnails>
  </main>
</template>

<script>
import Thumbnails from "./Thumbnails.vue";
export default {
  name: "Main-Component",
  components: { Thumbnails },

  props: {
    photos: Array,
    photoIndex: Number,
  },
  setup(props, context) {
    const getSelectedPhoto = () => {
      const selectedPhoto = props.photos.find(
        (photo) => photo.id == props.photoIndex
      );

      return selectedPhoto;
    };

    const changePhotoIndex = (photoId) => {
      context.emit("changePhotoIndex", photoId);
    };

    return { getSelectedPhoto, changePhotoIndex };
  },
};
</script>

<style lang="scss" scoped></style>
