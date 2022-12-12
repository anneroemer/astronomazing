<script setup lang="ts">
//import IconLogoPlanet from "@/components/icons/IconLogoPlanet.vue";
import axios from "axios";
import { ref } from "vue";

const query = ref();
console.log(query);

const loading = ref(false);

const queryResults = ref();

const getData = () => {
  axios
    .get(`https://images-api.nasa.gov/search?q=${query.value}`)
    .then((response) => {
      console.log("NASA query: ", response.data);
      queryResults.value = ref(response.data.collection.items);
      setTimeout(() => {
        loading.value = true;
      }, 1000);
    });
};
getData();
</script>

<template>
  <div>
    <input type="text" v-model="query" placeholder="Search..." />
    <button type="submit" @click="() => getData()">search</button>
    <p>{{ query }}</p>
    <ul>
      <li v-for="queryResult in queryResults" :key="queryResult.id">
        {{ queryResult.data }}
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss"></style>
