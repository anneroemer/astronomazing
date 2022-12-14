<script setup lang="ts">
import { ref } from "vue";

const props = defineProps<{
title: string;
description: string;
tags: string[];
date: string;
}>();

const descriptionText = ref(props?.description);
const text = descriptionText.value;

const textLimit = () => {
  if (!text) return;
  if (text.length > 170) {
    return text.slice(0, 140) + "...";
  } else {
    return text;
  }
};
textLimit();

</script>

<template>
    <li class="query-list-item">
        <h3>{{ title }}</h3>
        <p>{{ date }}</p>
        <p class="query-list-description">{{ textLimit() }}</p>
        <ul class="query-list-item-tags">
            <li v-for="tag in tags" class="query-list-item-tag">
                <p>{{ tag }}</p>
            </li>
        </ul>
    </li>
</template>

<style scoped>
.query-list-item {
  background-color: rgb(250, 248, 245);
  box-shadow: 4px 4px 0px #373bc8;
  padding: 1rem;
}
.query-list-description {
    padding: 0.5rem 0;
}
.query-list-item-tags {
    list-style: none;
    display: flex;
    flex-wrap: wrap;
    padding-left: 0;
    gap: 0.5rem;
}
.query-list-item-tag {
    padding: 0.2rem 0.4rem;
    background-color: rgba(55, 60, 200, 0.4);
    color: rgb(250, 248, 245);
}
</style>