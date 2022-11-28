<script setup>
import { NCard } from "naive-ui";

const props = defineProps(["image", "name"]);
</script>

<template>
  <NCard>
    <template #cover>
      <img :src="props.image" />
    </template>
    <h3>{{ props.name }}</h3>
    <slot></slot>
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
</style>
