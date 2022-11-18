<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";
import IconLogoPlanet from "../components/icons/IconLogoPlanet.vue";

const data = ref();
const loading = ref(false);

const created = () => {
  axios.get("https://go-apod.herokuapp.com/apod").then((response) => {
    console.log(response.data);
    data.value = ref(response.data);
    setTimeout(() => {
      loading.value = true;
    }, 1000);
  });
};
created();
</script>

<template>
  <main>
    <div class="home-image">
      <img
        v-if="loading"
        :src="data?.value.url"
        alt=""
        class="home-image-item"
      />
      <div v-if="!loading" class="icon-container">
        <component :is="IconLogoPlanet" color="#fff"></component>
      </div>
      <p v-if="loading" class="home-image-caption">
        {{ data?.value.date }} | {{ data?.value.title }}
      </p>
    </div>
  </main>
</template>

<style lang="scss">
.home-image {
  background-color: #373bc8;
  max-width: 350px;
  min-width: 300px;
  width: 100%;
  height: 400px;
  box-shadow: 4px 4px 0px #373bc8;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translate(-2px, -2px);
  &-item {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}
.home-image-caption {
  background-color: rgb(250, 248, 245);
  position: absolute;
  font-size: 0.8rem;
  letter-spacing: 2px;
  padding: 0.1rem 0.7rem;
  color: #373bc8;
  box-shadow: 4px 4px 0px #373bc8;
  bottom: 16px;
  right: -5px;
  z-index: 10;
}
.icon-container {
  width: 5rem;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  & svg {
    width: 100%;
    padding: 0rem 1rem 0.2rem;
    animation-duration: 7s;
    animation-name: movePlanet;
    animation-iteration-count: infinite;
    //animation-direction: alternate;
  }
}
@keyframes movePlanet {
  from {
    transform: rotate(360deg);
  }

  to {
    transform: rotate(45deg);
  }
}
@media screen and (min-width: 400px) {
  .home-image {
    min-width: 500px;
  }
}
</style>
