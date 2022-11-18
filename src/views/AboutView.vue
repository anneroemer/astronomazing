<script setup lang="ts">
import IconLogoPlanet from "@/components/icons/IconLogoPlanet.vue";
import axios from "axios";
import { ref } from "vue";
import IconArrow from "../components/icons/IconArrow.vue";
//import type { Component } from "vue";

const data = ref();
const loading = ref(false);

const created = () => {
  axios.get("https://go-apod.herokuapp.com/apod").then((response) => {
    //console.log(response.data);
    data.value = ref(response.data);
    loading.value = true;
  });
};
created();

const showText = ref(false);

const toggleText = () => {
  showText.value = !showText.value;
};
</script>

<template>
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
</template>

<style scoped lang="scss">
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
</style>
