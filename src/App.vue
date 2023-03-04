<template>
  <div class="py-5 vh-100 bg-light d-flex">
    <sidebar @changePhoto="changePhotoIndex" :photos="photos"></sidebar>
    <main-container
      @changePhotoIndex="changePhotoIndex"
      :photos="photos"
      :photoIndex="photoIndex"
    ></main-container>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";

import Sidebar from "./components/Sidebar.vue";
import MainContainer from "./components/MainContainer.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Sidebar,
    MainContainer,
  },
  setup() {
    // better to keep it in an .env
    const apiKey = "edPwNfx590enrwK5QBwcEFrYx07rNoAU7xhCBngzvKiEksJTq2askJtq";

    const photos = ref([]);

    const photoIndex = ref(0);

    const changePhotoIndex = (id) => {
      photoIndex.value = id;
    };

    const fetchPhotos = async () => {
      const headers = {
        Authorization: apiKey,
      };
      const params = {
        query: "nature",
        per_page: 3,
      };
      await axios
        .get(`https://api.pexels.com/v1/search`, {
          headers,
          params,
        })
        .then((res) => {
          photos.value = res.data.photos;
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      fetchPhotos().then(() => {
        photoIndex.value = photos.value[0].id;
      });
    });

    return { photos, photoIndex, changePhotoIndex };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
