<template>
  <div class="hero">
    <h1>{{ props.isBreakingBad ? "Breaking Bad" : "Rick and Morty" }}</h1>
    <p @click="emitSelectedShow">
      {{ props.isBreakingBad ? "Rick and Morty" : "Breaking Bad" }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps(["isBreakingBad"]);
const emit = defineEmits(["selectShow"]);

const emitSelectedShow = () => {
  emit("selectShow");
};
</script>

<style scoped lang="scss">
.hero {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  flex-direction: column;
  img {
    position: absolute;
    height: 700px;
    opacity: 0.1;
  }
  h1 {
    font-size: 55px;
    font-weight: bold;
  }
  p {
    cursor: pointer;
  }
}
</style>
