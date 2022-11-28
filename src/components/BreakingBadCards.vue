<script setup>
import { ref, watch } from "vue";
import axios from "axios";

import CardComponent from "@/components/CardComponent.vue";

const api = "https://www.breakingbadapi.com/api/characters?limit=8";

const characters = ref(null);
const page = ref(0);

const response = await axios.get(api);
characters.value = response.data;

watch(page, async () => {
  const res = await axios.get(`${api}&offset=${page.value * 8}`);
  characters.value = res.data;
});
</script>

<template>
  <div class="container">
    <div class="cards">
      <CardComponent
        v-for="character in characters"
        :key="character.char_id"
        :image="character.img"
        :name="character.name"
        :occupation="character.occupation"
      />
    </div>
    <div class="button-container">
      <button @click="page--"> &lt; </button>
      <button @click="page++"> > </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  background-color: rgb(27, 26, 26);
  padding: 30px;
}
.cards {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  h3 {
    font-weight: bold;
  }
  p {
    font-size: 10px;
  }
}

.jobs {
  display: flex;
  flex-wrap: wrap;
}
.button-container {
  display: flex;
  justify-content: center;
  padding-top: 30px;
  button {
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    margin: 0 5px;
    cursor: pointer;
  }
}
.spinner {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
