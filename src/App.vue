<template>
  <div>
    <MainScreen
      v-if="statusMatch === 'default'"
      @onStart="handleStartGame($event)"
    />
    <PlayScreen
      v-if="statusMatch === 'playing'"
      :cardsContext="settings.cardsContext"
      :totalBlocks="settings.totalBlocks"
      @onEndgame="handleEndGame"
      @rightSelect="handleRightSelect"
      @wrongSelect="handleWrongSelect"
    />
    <ResultScreen
      v-if="statusMatch === 'result'"
      :time="timer"
      @handlePlayAgain="handlePlayAgain"
    />
  </div>
  <div>
    <audio id="clap-sound">
      <source src="./assets/sounds/clap.mp3" type="audio/mp3" />
    </audio>
    <audio loop id="playing-sound">
      <source src="./assets/sounds/playing.mp3" type="audio/mp3" />
    </audio>
    <audio id="wrong-sound">
      <source src="./assets/sounds/wrong.mp3" type="audio/mp3" />
    </audio>
    <audio id="right-sound">
      <source src="./assets/sounds/right.mp3" type="audio/mp3" />
    </audio>
  </div>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import PlayScreen from "./components/PlayScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffle } from "./utils/array.js";

export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      timer: 0,
      settings: {
        totalBlocks: 0,
        cardsContext: [],
        startTime: 0,
      },
    };
  },
  components: {
    MainScreen,
    PlayScreen,
    ResultScreen,
  },
  methods: {
    handleStartGame(config) {
      this.settings.totalBlocks = config.totalBlocks;

      const firstCard = Array.from(
        { length: config.totalBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCard = [...firstCard];
      const cards = [...firstCard, ...secondCard];
      this.settings.cardsContext = shuffle(shuffle(shuffle(shuffle(cards))));
      this.settings.startTime = new Date().getTime();

      this.statusMatch = "playing";
      const playingSound = document.getElementById("playing-sound");
      playingSound.play();
    },
    handleEndGame() {
      this.timer = new Date().getTime() - this.settings.startTime;
      this.statusMatch = "result";
      const playingSound = document.getElementById("playing-sound");
      const clapSound = document.getElementById("clap-sound");
      playingSound.pause();
      playingSound.currentTime = 0;
      clapSound.play();
    },
    handlePlayAgain() {
      this.statusMatch = "default";
    },
    handleRightSelect() {
      const rightSound = document.getElementById("right-sound");
      rightSound.play();
    },
    handleWrongSelect() {
      const wrongSound = document.getElementById("wrong-sound");
      wrongSound.play();
    },
  },
};
</script>

<style></style>
