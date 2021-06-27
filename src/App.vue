<template>
  <div id="container" :style="{ backgroundColor: bgColor, color: color }">
    <!-- Header -->
    <div id="header">
      <div id="header-lines">
        <div class="header-line" />
        <div class="header-line" />
        <div class="header-line" />
        <div class="header-line" />
        <div class="header-line" />
        <div class="header-line" />
      </div>
      <div id="header-content">
        <div
          class="button-wrapper"
          :style="{ backgroundColor: bgColor, marginLeft: `20px` }"
        >
          <button
            @click.prevent="changeMode"
            class="button"
            style="color: blue"
          >
            {{ mode.toUpperCase() }}
          </button>
        </div>
        <div id="header-title" :style="{ backgroundColor: bgColor }">
          BITRACING
        </div>
        <div
          class="button-wrapper"
          :style="{ backgroundColor: bgColor, marginRight: `20px` }"
        >
          <button
            v-if="mode === 'racing'"
            @click.prevent="changeRacingState"
            class="button"
            style="color: black"
          >
            {{ racingState === "stopped" ? "PLAY" : "STOP" }}
          </button>
          <div id="color-buttons" v-else>
            <input
              type="color"
              class="color-input"
              id="input-bgColor"
              name="input-bgColor"
              v-model="bgColor"
            />
            <input
              type="color"
              class="color-input"
              id="input-color"
              name="input-color"
              v-model="color"
            />
          </div>
        </div>
      </div>
    </div>
    <!-- Main -->
    <div v-if="mode === 'running'" class="main">
      <div id="slider-container">
        <input
          class="slider"
          type="range"
          v-model="speed"
          min="0"
          max="100"
          step="1"
        />
        <div id="slider-text">{{ speed }} km/h</div>
      </div>
      <div id="text-input-container">
        <input type="text" placeholder="type..." id="text-input" :style="{ color: color }" />
      </div>
    </div>
    <div v-else id="racing-container">
      <div class="racing-row" style="lineHeight: 45px">
        <h3 class="racing-text" style="right: 18px; fontSize: 64px">
          HUMAN RUNNING
        </h3>
        <div class="racing-speed">10km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 25px">
        <h3
          class="racing-text"
          style="left: 110px; fontSize: 34px; lineHeight: 0.78em"
        >
          HIPPOPOTAMUS
        </h3>
        <div class="racing-speed">20km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 24px">
        <h3
          class="racing-text"
          style="right: 90px; fontSize: 34px; lineHeight: 0.76em"
        >
          TIGER
        </h3>
        <div class="racing-speed">50km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 46px">
        <h3
          class="racing-text"
          style="left: 25px; fontSize: 64px; lineHeight: 0.75em"
        >
          LION
        </h3>
        <div class="racing-speed">80km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 73px">
        <h3
          class="racing-text"
          style="right: 70px; fontSize: 100px; lineHeight: 0.74em"
        >
          SWIFT
        </h3>
        <div class="racing-speed">160km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 54px">
        <h3
          class="racing-text"
          style="left: 80px; fontSize: 75px; lineHeight: 0.75em"
        >
          FASTEST BICYCLE
        </h3>
        <div class="racing-speed">260km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 61px">
        <h3
          class="racing-text"
          style="right: 50px; fontSize: 87px; lineHeight: 0.75em"
        >
          FORMULA ONE
        </h3>
        <div class="racing-speed">370km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 53px; borderBottom: 1px solid black;">
        <h3
          class="racing-text"
          style="left: 30px; fontSize: 75px; lineHeight: 0.74em;"
        >
          AURBUS
        </h3>
        <div class="racing-speed">900km/h</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    const bgColor = ref("#dcdcdc");
    const color = ref("#0000ff");
    const mode = ref("racing");
    const racingState = ref("stopped");
    const speed = ref(0);

    function changeMode() {
      mode.value = mode.value === "racing" ? "running" : "racing";
    }

    function changeRacingState() {
      racingState.value =
        racingState.value === "stopped" ? "playing" : "stopped";
    }

    return {
      bgColor,
      color,
      mode,
      changeMode,
      changeRacingState,
      racingState,
      speed,
    };
  },
});
</script>

<style>
body {
  padding: 0;
  margin: 0;
}

@font-face {
  font-family: "Bitracing";
  src: url("~@/assets/fonts/BitracingGX.ttf") format("truetype-variations");
}

#app {
  font-family: "Bitracing", Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#container {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#header {
  margin: 40px auto;
  width: 98%;
  height: auto;
  position: relative;
}

#header-lines {
  position: absolute;
  top: 5px;
  left: 0;
  width: 100%;
}

.header-line {
  height: 0;
  border-top: 1px solid #a5a5a5;
  margin: 3px;
}

#header-content {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 10;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

#header-title {
  color: red;
  padding: 5px 10px;
  font-size: 24px;
}

.button-wrapper {
  padding: 0 6px;
}

.button {
  font-family: "Bitracing";
  background-color: #dcdcdc; /* Green */
  border-style: solid;
  border-width: 1px;
  border-color: white black black white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
  cursor: pointer;
}

#color-buttons {
  display: inline-flex;
  gap: 6px;
}

.color-input {
  padding: 0;
  height: 24px;
  width: 24px;
  border: none;
  cursor: pointer;
}
input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
  border: none;
}
input[type="color"]::-webkit-color-swatch {
  border: 1px solid black;
}
.main {
  display: flex;
  flex-direction: column;
  margin: 20px auto;
  width: 98%;
}

#slider-container {
  margin: 0 26px;
  padding: 3px 8px;
  background-color: #dcdcdc;
  border-style: solid;
  border-width: 1px;
  border-color: white black black white;
  text-align: center;
}
#slider-text {
  color: rgb(240, 73, 231);
  margin: 7px 0;
  font-size: 20px;
}
.slider {
  -webkit-appearance: none;
  width: 100%;
  appearance: none;
  background-color: rgb(240, 73, 231);
  color: rgb(240, 73, 231);
  height: 1.5px;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  cursor: pointer;
  background-color: rgb(240, 73, 231);
  color: rgb(240, 73, 231);
  width: 16px;
  height: 16px;
  border-radius: 50%;
}
.slider::-moz-range-thumb {
  cursor: pointer;
  background-color: rgb(240, 73, 231);
}
#text-input-container {
  margin: 60px 26px;
  background-color: transparent;
  text-align: center;
}
#text-input {
  font-family: "Bitracing";
  width: 99%;
  -webkit-appearance: none;
  border: none;
  outline: none;
  text-align: center;
  font-size: 250px;
  background-color: transparent;
}
#racing-container {
  width: 100%;
  margin-top: 60px;
}
.racing-row {
  border-top: 1px solid black;
  position: relative;
  height: auto;
}
.racing-speed {
  height: 100%;
  font-size: 16px;
  margin-left: 45px;
  color: cyan;
  text-shadow: #333333 1px 1px 3px;
}
.racing-text {
  margin-top: 0;
  margin-bottom: 0;
  position: absolute;
  line-height: 0.7em;
}
</style>
