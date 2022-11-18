<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const data = ref();

const created = () => {
  axios.get("https://go-apod.herokuapp.com/apod").then((response) => {
    console.log(response.data);
    data.value = ref(response.data);
  });
};
created();
</script>

<template>
  <main>
    <div class="home-image">
      <img :src="data?.value.url" alt="" class="home-image-item" />
    </div>
    <p>{{ data?.value.date }} | {{ data?.value.title }}</p>
  </main>
</template>

<style lang="scss">
.home-image {
  height: 400px;
  overflow: hidden;
  &-item {
    max-width: 500px;
    width: 100%;
    height: auto;
    object-fit: fill;
  }
}
</style>
