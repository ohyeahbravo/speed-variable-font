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
              value="color"
            />
          </div>
        </div>
      </div>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  data() {},
  setup() {
    const bgColor = ref("#dcdcdc");
    const color = ref("blue");
    const mode = ref("racing");
    const racingState = ref("stopped");

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
    };
  },
});
</script>

<style>
body {
  padding: 0;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
  background-color: #dcdcdc; /* Green */
  border-style: 1px solid;
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
  -webkit-appearance: none;
  border: none;
  margin: 0;
  outline: none;
}

input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
  margin: 0;
  border: none;
  box-shadow: 0;
}
input[type="color"]::-webkit-color-swatch {
  margin: 0;
  padding: 0;
  border: 1px solid black;
  cursor: pointer;
}
</style>
