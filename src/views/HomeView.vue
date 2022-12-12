<script setup lang="ts">
import axios from "axios";
import IconArrow from "../components/icons/IconArrow.vue";

import { ref } from "vue";
import IconLogoPlanet from "../components/icons/IconLogoPlanet.vue";

const data = ref();
const loading = ref(false);

const getData = () => {
  axios
    .get(
      `https://api.nasa.gov/planetary/apod?api_key=g4Cgb4KqIZPEorx3unUxCCGPkqxRa0bupphRQ5r7`
    )
    .then((response) => {
      console.log("NASA: ", response.data);
      data.value = ref(response.data);
      setTimeout(() => {
        loading.value = true;
      }, 1000);
    });
};
getData();

const showText = ref(false);

const toggleText = () => {
  showText.value = !showText.value;
};
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
    <div class="about" :class="{ animateheight: loading }">
      <div class="icon-planet-container">
        <component
          v-if="!loading"
          :is="IconLogoPlanet"
          class="icon-planet"
          color="#373bc8"
        ></component>
      </div>
      <h1 class="about-headline">{{ data?.value.title }}</h1>
      <p v-if="showText" class="about-text">{{ data?.value.explanation }}</p>
      <p v-else class="about-text">
        {{ data?.value.explanation.slice(0, 300) + "..." }}
      </p>
      <button @click="toggleText" class="about-btn">
        <component
          :is="IconArrow"
          class="icon-arrow"
          :class="{ arrowUp: showText }"
        ></component>
      </button>
    </div>
  </main>
</template>

<style lang="scss">
main {
  gap: 1rem;
}
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
.about {
  background-color: rgb(250, 248, 245);
  padding: 1rem 3rem 1rem 1.5rem;
  max-width: 500px;
  min-height: 400px;
  width: 100%;
  //height: fit-content;
  box-shadow: 4px 4px 0px #373bc8;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  transition: 0.4s;
  &-headline {
    font-size: 1.5rem;
    color: #373bc8;
  }
  &-text {
    font-size: 1rem;
    color: #373bc8;
  }
}
.animateHeight {
  height: fit-content;
  transition: 0.4s;
}
.about-btn {
  all: unset;
  height: 50px;
  width: 50px;
  /* box-shadow: 4px 4px 0px #373bc8; */
  background-color: #373bc8;
  position: absolute;
  top: 30%;
  right: -10px;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: scaleY(1);
  transition: all 0.4s;
}
.arrowUp {
  transform: scaleY(-1);
  transition: all 0.4s;
}
.icon-arrow {
  fill: #fff;
}
.icon-planet-container {
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
