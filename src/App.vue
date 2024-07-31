<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandBeforeStart($event)"
  />
  <interact-sreen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
  <copy-right-screen />
</template>
<script>
import MainScreen from "./components/MainScreen.vue";
import InteractSreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import CopyRightScreen from "./components/CopyRightScreen.vue";
import { shuffled } from "./utils/array";
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  components: {
    MainScreen,
    InteractSreen,
    ResultScreen,
    CopyRightScreen,
  },
  methods: {
    onHandBeforeStart(config) {
      console.log("running handle before start", config);
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCart = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCard = [...firstCart];
      const cards = [...firstCart, ...secondCard];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      this.settings.startedAt = new Date().getTime();
      // data ready
      this.statusMatch = "match";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;

      this.statusMatch = "result";
    },
  },
};
</script>
