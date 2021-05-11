<template>
  <div class="hello mt-3">
    <h3 class="title is-3">{{ text }}</h3>
    <h3 class="title is-1">{{ minutes }} : {{ seconds }}</h3>
    <div class="buttons">
      <b-button type="is-primary" v-if="!started" @click="start"
        >Start</b-button
      >
      <b-button type="is-warning" v-else @click="pause">Pause</b-button>
      <b-button type="is-danger" @click="reset">Reset</b-button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
/* eslint-disable */
const prepTimeEndSound = new Audio(require("@/assets/prepTimeFinished.wav"));
const totalTimerFinishedSound = new Audio(
  require("@/assets/timerFinished.wav")
);

export default Vue.extend({
  name: "Timer",
  data() {
    return {
      countDown: 10 * 60,
      started: false,
    };
  },
  computed: {
    minutes() {
      return Math.floor(this.countDown / 60);
    },
    seconds() {
      const output = this.countDown % 60;
      return output > 9 ? output : `0${output}`;
    },
    text() {
      if (this.countDown === 10 * 60) {
        return "Not Started Yet";
      } else if (this.countDown > 8 * 60) {
        return "Preparation Time";
      } else if (this.countDown === 0) {
        return "Finished";
      } else {
        return "Consulation";
      }
    },
  },
  methods: {
    countDownTimer() {
      setTimeout(() => {
        if (this.started) {
          this.countDown -= 1;

          if (this.countDown === 8 * 60) {
            prepTimeEndSound.play();
          }

          if (this.countDown === 0) {
            totalTimerFinishedSound.play();
            this.started = false;
          }
        }
        this.countDownTimer();
      }, 1000);
    },
    start() {
      this.started = true;
    },
    pause() {
      this.started = false;
    },
    hitSpace() {
      this.started = !this.started;
    },
    reset() {
      if (
        this.countDown === 0 ||
        window.confirm("Are you sure that you want to reset?")
      ) {
        this.started = false;
        this.countDown = 10 * 60;
      }
    },
  },
  created() {
    this.countDownTimer();
    window.addEventListener("keydown", (e) => {
      e.preventDefault();
      if (e.keyCode === 32) {
        this.hitSpace();
      }
    });
  },
});
</script>
<style>
.buttons {
  margin-left: auto;
  align-items: center;
  display: flex;
  flex-wrap: wrap;
  justify-content: center !important;
}
</style>
