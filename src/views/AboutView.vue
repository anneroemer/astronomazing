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
  <div class="about">
    <h1>{{ data?.value.title }}</h1>
    <p>{{ data?.value.explanation }}</p>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
