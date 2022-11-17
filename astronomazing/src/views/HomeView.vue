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
    <div>
      <div class="home-image">
        <img :src="data?.value.url" alt="" class="home-image-item" />
      </div>
      <p>{{ data?.value.date }} | {{ data?.value.title }}</p>
      <p>{{ data?.value.explanation }}</p>
    </div>
  </main>
</template>

<style lang="scss">
.home-image {
  max-width: 500px;
  //width: 100%;
  height: 200px;
  &-item {
    width: 100%;
    height: auto;
    object-fit: cover;
  }
}
</style>
