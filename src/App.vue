<script setup>
import BreakingBadCardsSuspence from "@/components/BreakingBadCardsSuspence.vue";
import RickAndMortyCards from "@/components/RickAndMortyCards.vue";
import HeroComponent from "@/components/HeroComponent.vue";
import { ref } from "vue";

const isBreakingBad = ref(true);
</script>

<template>
  <main>
    <HeroComponent
      :isBreakingBad="isBreakingBad"
      @selectShow="isBreakingBad = !isBreakingBad"
    />
    <KeepAlive>
      <Component
        :is="isBreakingBad ? BreakingBadCardsSuspence : RickAndMortyCards"
      />
    </KeepAlive>
  </main>
</template>
