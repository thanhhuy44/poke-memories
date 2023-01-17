/* eslint-disable */
<template>
  <div class="card w-full">
    <div
      class="card__inner"
      :class="{ card__flip: isFlipped, card__disable: isDisabled }"
      @click="handleToggleCard"
    >
      <div class="card__face md:p-3 card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face md:p-3 card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/images/' +
              imageName.card +
              '.png')})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  props: {
    imageName: {
      type: Object,
    },
  },
  methods: {
    handleToggleCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onFlip", this.imageName);
      }
    },
    handleCloseCard() {
      setTimeout(() => {
        this.isFlipped = false;
      }, 1000);
    },
    handleDisableCard() {
      this.isDisabled = true;
    },
    handleEnableCard() {
      this.isDisabled = false;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: flex;
  align-items: center;
}

.card__inner {
  width: 90px;
  height: 120px;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__inner.card__disable {
  cursor: default;
}

.card__inner.card__flip {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 16px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
  background-color: white;
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40px 60px;
  height: 100%;
  width: 100%;
}

.card__face--back {
  transform: rotateY(180deg);
  height: 100%;
  width: 100%;
}
.card__face--back .card__content {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 100px;
  width: 100%;
}
</style>
