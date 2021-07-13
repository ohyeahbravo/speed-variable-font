<template>
  <div id="container">
    <!-- Header -->
    <div id="header">
      <div id="header-title">BITRACING</div>
      <div class="button-wrapper">
        <a
          @click="toggleAboutDialog"
          style="margin-right: 15px; cursor: pointer"
        >
          <img
            src="@/assets/images/about.svg"
            style="height: 45px; width: auto; object-fit: contain"
          />
        </a>
        <a @click="changeMode" style="cursor: pointer">
          <img
          v-if="mode==='racing'"
            src="@/assets/images/speed-comparison.svg"
            style="width: auto; height: 45px; object-fit: contain"
          />
          <img
          v-else
            src="@/assets/images/type-yourself.svg"
            style="width: auto; height: 45px; object-fit: contain"
          />
        </a>
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
          @change="getOverflow"
        />
        <div id="slider-text">{{ speed }} km/h</div>
      </div>
      <div id="text-input-container">
        <input
          type="text"
          placeholder="type..."
          id="text-input"
          spellcheck="false"
          :style="[
            {
              fontVariationSettings: `'slnt' ${speed}`,
            },
            speed >= 1
              ? `animation: slider ${
                  30 - (29.9 / 900) * speed * 0.98
                }s linear infinite`
              : '',
          ]"
        />
      </div>
    </div>
    <div v-else id="racing-container">
      <div class="racing-row">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-800px',
              fontSize: '85px',
              color: 'rgb(0, 255, 0)',
              lineHeight: '0.64em',
              fontVariationSettings: `'slnt' 10`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 20s linear infinite'
              : '',
          ]"
        >
          HUMAN RUNNING
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/10km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/10km.png"
            style="width: auto; height: 53px; object-fit: contain; margin-left: 15px;"
          />
        </div>
      </div>
      <div class="racing-row">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-670px',
              fontSize: '85px',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 20`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 18s linear infinite'
              : '',
          ]"
        >
          BLACK MAMBA
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/20km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/20km.png"
            style="width: auto; height: 54px; object-fit: contain; margin-left: 780px;"
          />
        </div>
      </div>
      <div class="racing-row" :style="{ lineHeight: '53px' }">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-310px',
              fontSize: '85px',
              color: 'rgb(0, 255, 0)',
              lineHeight: '0.64em',
              fontVariationSettings: `'slnt' 50`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 13s linear infinite'
              : '',
          ]"
        >
          TIGER
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/50km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/50km.png"
            style="width: auto; height: 53px; object-fit: contain; margin-left: 450px;"
          />
        </div>
      </div>
      <div class="racing-row">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-250px',
              fontSize: '85px',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 80`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 10s linear infinite'
              : '',
          ]"
        >
          LION
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/80km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/80km.png"
            style="width: auto; height: 54px; object-fit: contain; margin-left: 270px;"
          />
        </div>
      </div>
      <div class="racing-row">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-320px',
              fontSize: '85px',
              color: 'rgb(0, 255, 0)',
              lineHeight: '0.64em',
              fontVariationSettings: `'slnt' 170`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 6s linear infinite'
              : '',
          ]"
        >
          SWIFT
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/170km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/170km.png"
            style="width: auto; height: 53px; object-fit: contain; margin-left: 720px;"
          />
        </div>
      </div>
      <div class="racing-row">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-900px',
              fontSize: '85px',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 300`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 3s linear infinite'
              : '',
          ]"
        >
          FORMULA 1 CAR
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/300km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/300km.png"
            style="width: auto; height: 54px; object-fit: contain; margin-left: 620px;"
          />
        </div>
      </div>
      <div class="racing-row" :style="{ lineHeight: '53px' }">
        <h3
          class="racing-text"
          :style="[
            {
              right: '-1050px',
              fontSize: '85px',
              color: 'rgb(0, 255, 0)',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 420`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 2s linear infinite'
              : '',
          ]"
        >
          BUGATTI VEYRON
        </h3>
        <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/420km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/420km.png"
            style="width: auto; height: 53px; object-fit: contain; margin-left: 90px;"
          />
        </div>
      </div>
      <div
        class="racing-row"
        style="lineHeight: 53px;"
      >
        <h3
          class="racing-text"
          :style="[
            {
              right: '-600px',
              fontSize: '85px',
              lineHeight: '0.63em',
              fontVariationSettings: `'slnt' 900`,
            },
            racingState !== 'stopped'
              ? 'animation: moving 1s linear infinite'
              : '',
          ]"
        >
          AURBUS
        </h3>
       <div class="racing-speed" :style="{ height: '53px' }">
          <img
            src="@/assets/images/900km.svg"
            style="width: auto; height: 45px; object-fit: contain; margin-top: 4px; z-index: 40;"
          />
          <img
            src="@/assets/images/900km.png"
            style="width: auto; height: 54px; object-fit: contain; margin-left: 880px;"
          />
        </div>
      </div>
      <div
        class="racing-row"
        style="padding: 30px; display: flex; align-items: center; justify-content: center;"
      >
      <img
            src="@/assets/images/ending.svg"
            style="width: 100%; height: auto; object-fit: fill;"
          />
      </div>
    </div>
  </div>
  <!-- About Dialog -->
  <div v-if="dialogOpen" id="dialog">
    <div style="display: flex; flex-direction: row; align-items: start">
      <div style="display: block; line-height: 24px">
        <p style="margin: 0 15px 0 0; text-align: left; letter-spacing: 0.9px">
          <strong>Bitracing</strong> is a typeface that expresses
          <i>speed</i> with letters. The basic shape of the typeface is inspired
          by motion blur, which graphically depicts the visual effects of
          movement. This is a variable font with speeds from 0 to 900 km/h as the
          axis. As the speed increases, the typeface becomes increasingly
          illegible.
        </p>
      </div>
      <div style="display: flex; flex-direction: column; align-items: start">
        <img
          src="@/assets/images/about1.png"
          style="width: 270px; height: auto; object-fit: contain"
        />
        <p style="font-size: 8pt; margin: 0; padding-top: 3px">
          © David Ramos/Getty Images
        </p>
      </div>
    </div>
    <img
      src="@/assets/images/about2.svg"
      style="width: 650px; height: auto; object-fit: cover; margin-top: 15px"
    />
    <div
      style="
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
      "
    >
      <p>Designed by Hyun-jeong Cho</p>
      <p style="padding-left: 10px">zo-hj.com</p>
      <p>© 2021</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    const mode = ref("racing");
    const racingState = ref("playing");
    const speed = ref(0);
    const overflow = ref(0);
    const dialogOpen = ref(false);

    function changeMode() {
      mode.value = mode.value === "racing" ? "running" : "racing";
    }

    function getOverflow() {
      const element = document.querySelector("#text-input");
      overflow.value = element.scrollWidth - element.clientWidth;
      console.log(overflow.value);
    }

    watch(overflow, (newOverflow) => {
      console.log(newOverflow);
    });

    function toggleAboutDialog() {
      dialogOpen.value = !dialogOpen.value;
    }

    return {
      overflow,
      mode,
      changeMode,
      racingState,
      speed,
      getOverflow,
      toggleAboutDialog,
      dialogOpen,
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
  background-color: white;
}

#header {
  margin: 0;
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}

#header-title {
  color: black;
  padding: 30px;
  font-size: 24px;
}

.button-wrapper {
  padding-top: 15px;
  padding-right: 35px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
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
  color: black;
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

::-webkit-input-placeholder {
  /* Edge */
  color: black;
}

:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: black;
}

::placeholder {
  color: black;
}

.main {
  display: flex;
  flex-direction: column;
  margin: 20px auto;
  width: 100%;
}

#slider-container {
  margin: 0 26px;
  padding: 3px 8px;
  text-align: center;
}
#slider-text {
  color: rgb(0, 255, 0);
  margin: 7px 0;
  font-size: 20px;
}
.slider {
  -webkit-appearance: none;
  width: 100%;
  appearance: none;
  background-color: rgb(0, 255, 0);
  color: rgb(0, 255, 0);
  height: 1.5px;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  cursor: pointer;
  background-color: rgb(0, 255, 0);
  color: rgb(0, 255, 0);
  width: 16px;
  height: 16px;
  border-radius: 50%;
}
.slider::-moz-range-thumb {
  cursor: pointer;
  background-color: rgb(0, 255, 0);
}
#text-input-container {
  margin: 32px 26px;
  background-color: transparent;
}

#text-input {
  font-family: "Bitracing";
  width: 100%;
  -webkit-appearance: none;
  border: none;
  outline: none;
  text-align: center;
  position: relative;
  font-size: 250px;
  background-color: transparent;
  overflow: visible;
  /* outline: 1px dashed black;
  outline-offset: -100px;
  padding-left: 100px; */
}
#racing-container {
  width: 100%;
  margin-top: 35px;
}
.racing-row {
  border-top: 1px solid black;
  position: relative;
  height: auto;
  line-height: 54px;
}
.racing-speed {
  margin: 0 0 0 20px;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0;
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
    transform: translateX(-200vw);
  }
}
@keyframes slider {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-100%);
  }
}

#dialog {
  position: absolute;
  width: 650px;
  height: 350px;
  background-color: rgb(0, 255, 0);
  top: 80px;
  right: 45px;
  z-index: 50;
  border: 2px black solid;
  padding: 15px;
  font-family: Helvetica, sans-serif;
  display: flex;
  flex-direction: column;
  font-size: 14pt;
}
</style>
