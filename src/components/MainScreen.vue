<template>
  <div class="main-container">
    <h1 class="text-3xl font-bold">Poke Memories</h1>
    <p class="my-8">Select mode to start game:</p>
    <div class="mode grid grid-cols-1 sm:grid-cols-4 gap-2">
      <button
        class="p-1 border border-gray-200 hover:bg-green-200"
        @click="onStart(16)"
      >
        <p>4 x 4</p>
        <p>Easy</p>
      </button>
      <button
        class="p-1 border border-gray-200 hover:bg-green-200"
        @click="onStart(36)"
      >
        <p>6 x 6</p>
        <p>Normal</p>
      </button>
      <button
        class="p-1 border border-gray-200 hover:bg-green-200"
        @click="onStart(64)"
      >
        <p>8 x 8</p>
        <p>Hard</p>
      </button>
      <button
        class="p-1 border border-gray-200 hover:bg-green-200"
        @click="onStart(100)"
      >
        <p>10 x 10</p>
        <p>Super Hard</p>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(blocks) {
      this.$emit("onStart", { totalBlocks: blocks });
    },
  },
};
</script>

<style lang="css" scoped>
.main-container {
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
