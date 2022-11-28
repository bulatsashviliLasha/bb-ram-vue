<script setup>
import { ref, watch, onBeforeMount } from "vue";
import axios from "axios";
import { NSpin } from "naive-ui";
import CardComponent from "@/components/CardComponent.vue";
import scrollTop from "@/utils/scroll-top";

const characters = ref(null);
const page = ref(1);

watch(page, async () => {
  const res = await axios.get(
    `https://rickandmortyapi.com/api/character/?page=${page.value}`
  );
  characters.value = res.data.results;
});

const scrollUpAndDecreasePage = () => {
  page.value--;
  scrollTop();
}
const scrollUpAndIncreasePage = () => {
  page.value++;
  scrollTop();
}
onBeforeMount(async () => {
  const response = await axios.get("https://rickandmortyapi.com/api/character");
  characters.value = response.data.results;
});
</script>

<template>
  <div class="container">
    <div v-if="characters" class="cards">
      <CardComponent
        v-for="character in characters"
        :key="character.char_id"
        :image="character.image"
        :name="character.name"
      >
        <p>{{ character?.location?.name }}</p>
      </CardComponent>
    </div>
    <div v-else class="cards spinner">
      <NSpin size="large" />
    </div>
    <div class="button-container">
      <button :class="{'btn-disabled': page === 1}" :disabled="page === 1" @click="scrollUpAndDecreasePage">&lt;</button>
      <button :class="{'btn-disabled': page === 42}" :disabled="page === 42" @click="scrollUpAndIncreasePage">></button>
    </div>
  </div>
</template>
