<template>
  <div id="app">
    <taskbar v-on:onclicktaskbar="onClickTaskBarItem" />
    <component v-for="i in windows" v-bind:key="i.id" v-bind:is="i.main">
      <button id="lk" @click="addElem">CLick vue</button>
    </component>

    <startMenu />
  </div>
</template>

<script>
import taskbar from "./components/taskbar";
import startMenu from "./components/startmenu";
import window from "./components/window";

export default {
  name: "App",
  components: {
    taskbar,
    startMenu,
    window,
  },
  data() {
    return { windows: [] };
  },
  methods: {
    onClickTaskBarItem: function (itemName) {
      this.windows.push({ main: window, id: this.windows.length + 1 });
      console.log(itemName);
      if (this.windows.length > 10) {
        this.windows.pop();
      }
    },
  },

};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
