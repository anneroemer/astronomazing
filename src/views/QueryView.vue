<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const props = defineProps<{
  title: string;
  description: string;
  tags: string[];
  date: string;
  id: string;
}>();

//nasa_id
const query = ref(props.id);
console.log(query.value);
const loading = ref(false);
const queryResults = ref();
const queryImage = ref();

//"https://images-assets.nasa.gov/image/GSFC_20171208_Archive_e000146/collection.json"
//"https://images-assets.nasa.gov/image/GSFC_20171208_Archive_e000146/collection.json"

const getData = () => {
  queryResults.value = [];
  axios
    .get(`https://images-api.nasa.gov/search?q=${query.value}`)
    .then((response) => {
      //console.log("NASA query: ", response.data);
      queryResults.value = ref(response.data.collection.items[0].data);
      queryImage.value = ref(response.data.collection.items[0].href);
      console.log(response.data.collection.items[0].href);
      console.log(response.data.collection.items);
      setTimeout(() => {
        loading.value = true;
      }, 1000);
    });
};
getData();
</script>
<template>
  <img :src="queryImage.value[0]" alt="" />
  <div v-for="queryResult in queryResults.value">
    <h1>{{ queryResult.title }}</h1>
    <h3>{{}}</h3>
    <p>{{ date }}</p>
    <p class="query-list-description">{{ description }}</p>
    <ul class="query-list-item-tags">
      <li v-for="tag in tags" class="query-list-item-tag">
        <p>{{ tag }}</p>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
