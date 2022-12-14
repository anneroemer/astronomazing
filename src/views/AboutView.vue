<script setup lang="ts">
//import IconLogoPlanet from "@/components/icons/IconLogoPlanet.vue";
import QueryItem from "@/components/QueryItem.vue";
import { RouterLink } from "vue-router";
import axios from "axios";
import { ref } from "vue";

const query = ref();
const loading = ref(false);
const queryResults = ref();

const getData = () => {
  queryResults.value = [];
  axios
    .get(`https://images-api.nasa.gov/search?q=${query.value}`)
    .then((response) => {
      //console.log("NASA query: ", response.data);
      queryResults.value = ref(response.data.collection.items);
      console.log(response.data.collection.items)
      setTimeout(() => {
        loading.value = true;
      }, 1000);
    });
};
getData();

</script>

<template>
  <div class="query">
    <div class="query-field">
      <input type="text" v-model="query" placeholder="Search..." />
      <button type="submit" @click="() => getData()">search</button>
    </div>
    <h1 v-if="loading" >Results for {{ query }}</h1>
    <ul v-if="loading" class="query-list">
        <template v-for="queryResult, index in queryResults.value" :key="index" class="query-list-item">
          <template v-for="item in queryResult.data">
            <RouterLink :to="'/about/' + item.nasa_id" :title="item.title" :description="item.description" :tags="item.keywords" :date="item.date_created">
              <QueryItem :title="item.title" :description="item.description" :tags="item.keywords" :date="item.date_created" />
            </RouterLink>
          </template>
        </template>
    </ul>
  </div>
</template>

<style scoped lang="scss">
.query {
  max-width: 500px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.query-field {
  display: flex;
  width: 100%;
  & input {
    all: unset;
    background-color: rgb(250, 248, 245);
    width: 100%;
  }
}
.query-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  list-style: none;
  padding-left: 0;
  gap: 1rem;
}
</style>
