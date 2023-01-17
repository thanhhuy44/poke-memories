<template>
  <div class="flex justify-center">
    <div class="play-container inline-block mx-auto">
      <h1 class="text-3xl text-center my-8">Good Luck! 🐥🐧</h1>
      <div class="grid gap-4" :class="`grid-cols-${Math.sqrt(totalBlocks)}`">
        <CardItem
          v-for="(card, index) in cardsContext"
          :key="index"
          :imageName="{ index, card }"
          :ref="`card-${index}`"
          @onFlip="checkingCard"
        />
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";

export default {
  data() {
    return {
      checkingArr: [],
    };
  },
  components: {
    CardItem,
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
    totalBlocks: {
      require: true,
      type: Number,
    },
  },
  methods: {
    checkingCard(card) {
      if (this.checkingArr.length === 0) {
        this.checkingArr.push(card);
        this.$refs[`card-${this.checkingArr[0].index}`][0].handleDisableCard();
        return;
      }
      if (this.checkingArr.length === 1) {
        this.checkingArr.push(card);
        if (this.checkingArr[0].card === this.checkingArr[1].card) {
          this.$emit("rightSelect");
          this.$refs[
            `card-${this.checkingArr[0].index}`
          ][0].handleDisableCard();
          this.$refs[
            `card-${this.checkingArr[1].index}`
          ][0].handleDisableCard();
          const cardDisables = document.querySelectorAll(
            ".play-container .card .card__inner.card__disable"
          );
          if (
            cardDisables &&
            cardDisables.length === this.cardsContext.length - 1
          ) {
            setTimeout(() => {
              this.$emit("onEndgame");
            }, 1200);
          }
        } else {
          this.$emit("wrongSelect");
          this.$refs[`card-${this.checkingArr[0].index}`][0].handleEnableCard();
          this.$refs[`card-${this.checkingArr[0].index}`][0].handleCloseCard();
          this.$refs[`card-${this.checkingArr[1].index}`][0].handleCloseCard();
        }
        this.checkingArr = [];
      }
    },
  },
};
</script>
