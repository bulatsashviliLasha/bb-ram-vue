<script setup>
import BreakingBadCards from "@/components/BreakingBadCards.vue";
import { NSpin } from "naive-ui";
</script>
<template>
  <Suspense>
    <template #default>
      <BreakingBadCards />
    </template>
    <template #fallback>
      <div class="cards">
        <NSpin size="large" stroke="white" />
      </div>
    </template>
  </Suspense>
</template>

<style scoped>
.cards {
  background-color: rgb(27, 26, 25);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 700px;
}
</style>
