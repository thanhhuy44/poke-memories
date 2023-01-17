<template>
  <div class="result-container">
    <h1 class="text-3xl font-bold">✨ Victory ✨</h1>
    <p class="my-2">Time: {{ time / 1000 }}s</p>
    <button
      class="p-1 border border-gray-200 hover:bg-green-200 mt-8"
      @click="handlePlayAgain()"
    >
      Play Again
    </button>
  </div>
</template>

<script>
export default {
  props: {
    time: {
      require: true,
    },
  },
  methods: {
    handlePlayAgain() {
      this.$emit("handlePlayAgain");
    },
  },
};
</script>

<style lang="css" scoped>
.result-container {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
</style>
