<template>
  <div id="container" :style="{ backgroundColor: bgColor, color: color }">
    <!-- Header -->
    <div id="header">
      <div
        class="button-wrapper"
        :style="{ backgroundColor: bgColor, marginLeft: `20px` }"
      >
        <button @click.prevent="changeMode" class="button" style="color: blue">
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
          {{ racingState === "stopped" ? "GO" : "STOP" }}
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
    <!-- Main -->
    <div v-if="mode === 'running'" class="main">
      <div id="slider-container">
        <input
          class="slider"
          type="range"
          v-model="speed"
          min="0"
          max="900"
          step="1"
        />
        <div id="slider-text">{{ speed }} km/h</div>
      </div>
      <div id="text-input-container">
        <input
          type="text"
          placeholder="type..."
          id="text-input"
          :style="[
            {
              color: color,
              fontVariationSettings: `'slnt' ${speed}`,
            },
            speed >= 1
              ? `animation: slider ${
                  30 - (29.9 / 900) * speed
                }s linear infinite`
              : '',
          ]"
        />
      </div>
    </div>
    <div v-else id="racing-container">
      <div class="racing-row" style="lineHeight: 39px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '64px',
              lineHeight: '0.62em',
              fontVariationSettings: `'slnt' 10`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 20s linear infinite'
              : '',
          ]"
        >
          HUMAN RUNNING
        </h3>
        <div class="racing-speed">10km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 21px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '34px',
              lineHeight: '0.66em',
              fontVariationSettings: `'slnt' 20`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 18s linear infinite'
              : '',
          ]"
        >
          HIPPOPOTAMUS
        </h3>
        <div class="racing-speed">20km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 21px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '34px',
              lineHeight: '0.6em',
              fontVariationSettings: `'slnt' 50`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 13s linear infinite'
              : '',
          ]"
        >
          TIGER
        </h3>
        <div class="racing-speed">50km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 40px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '64px',
              lineHeight: '0.64em',
              fontVariationSettings: `'slnt' 80`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 10s linear infinite'
              : '',
          ]"
        >
          LION
        </h3>
        <div class="racing-speed">80km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 62px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '107px',
              lineHeight: '0.61em',
              fontVariationSettings: `'slnt' 160`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 6s linear infinite'
              : '',
          ]"
        >
          SWIFT
        </h3>
        <div class="racing-speed">160km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 47px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '75px',
              lineHeight: '0.64em',
              fontVariationSettings: `'slnt' 260`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 3s linear infinite'
              : '',
          ]"
        >
          FASTEST BICYCLE
        </h3>
        <div class="racing-speed">260km/h</div>
      </div>
      <div class="racing-row" style="lineHeight: 53px">
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '87px',
              lineHeight: '0.61em',
              fontVariationSettings: `'slnt' 370`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 2s linear infinite'
              : '',
          ]"
        >
          FORMULA ONE
        </h3>
        <div class="racing-speed">370km/h</div>
      </div>
      <div
        class="racing-row"
        style="lineHeight: 46px; borderbottom: 1px solid black"
      >
        <h3
          class="racing-text"
          :style="[
            {
              left: '0',
              fontSize: '75px',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 900`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 0.5s linear infinite'
              : '',
          ]"
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
  overflow: hidden;
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
  font-weight: normal;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#header {
  padding: 40px 15px;
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
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
  font-weight: normal;
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
  margin: 32px 26px;
  background-color: transparent;
}

#text-input {
  font-family: "Bitracing";
  width: 99%;
  -webkit-appearance: none;
  border: none;
  outline: none;
  text-align: start;
  position: relative;
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
  z-index: 20;
  text-shadow: #333333 1px 1px 3px;
}
.racing-text {
  font-weight: normal;
  margin-top: 0;
  margin-bottom: 0;
  position: absolute;
}
@keyframes moving {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100vw);
  }
}
@keyframes slider {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100%);
  }
}
</style>
