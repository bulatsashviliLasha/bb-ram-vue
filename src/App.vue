<script setup>
import BreakingBadCards from "@/components/BreakingBadCards.vue"
</script>

<template>
  <main>
    <Suspense>
      <template #default>
        <BreakingBadCards/>
      </template>
      <template #fallback>
        <div>
          <div>Loading...</div>
        </div>
      </template>
    </Suspense>
  </main>
</template>

