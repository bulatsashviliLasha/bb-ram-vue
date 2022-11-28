<script setup>
import { ref, watch } from "vue";
import axios from "axios";
import CardComponent from "@/components/CardComponent.vue";
import scrollTop from "@/utils/scroll-top";

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
    <div v-if="characters" class="cards">
      <CardComponent
        v-for="character in characters"
        :key="character.char_id"
        :image="character.img"
        :name="character.name"
      >
        <div class="jobs">
          <p v-for="(job, index) in character.occupation" :key="job + index">
            {{ job
            }}<span v-if="index < character.occupation.length - 1">, </span>
          </p>
        </div>
      </CardComponent>
    </div>
    <div else>No more characters {{ page }}</div>
    <div class="button-container">
      <button
        :class="{ 'btn-disabled': page === 0 }"
        :disabled="page === 0"
        @click="
          page--;
          scrollTop();
        "
      >
        &lt;
      </button>
      <button
        :class="{ 'btn-disabled': page === 7 }"
        :disabled="page === 7"
        @click="
          page++;
          scrollTop();
        "
      >
        >
      </button>
    </div>
  </div>
</template>
