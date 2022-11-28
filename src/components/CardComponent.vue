<script setup>
import { NCard } from "naive-ui";

const props = defineProps(["image", "name", "occupation"]);
</script>

<template>
  <NCard>
    <template #cover>
      <img :src="props.image" />
    </template>
    <h3>{{ props.name }}</h3>
    <div class="jobs">
      <p v-for="(job, index) in props.occupation" :key="job + index">
        {{ job }}<span v-if="index < occupation.length - 1">, </span>
      </p>
    </div>
  </NCard>
</template>

<style lang="scss" scoped>
.n-card {
  width: 200px;
  margin: 10px 20px;
  img {
    height: 250px;
    object-fit: cover;
  }
}

p {
  font-size: 10px;
}

.jobs {
  display: flex;
  flex-wrap: wrap;
}
</style>
