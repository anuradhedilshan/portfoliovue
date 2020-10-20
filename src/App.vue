<template>
  
  <div id="app">
    <taskbar v-on:onmenuclick="is = !is" v-on:onclicktaskbar="onClickTaskBarItem" />
 
    <!-- v-bind:isopen="isopen" -->
    <component
      v-for="i in windows"
      v-bind:key="i.id"
      v-on:minimizeone="onminimizeone"
      v-bind:is="i.window"
      v-bind:id="i.id"
    >
    
    </component>
 <icons />
    <startMenu v-if="is" v-bind:class="{'open':is}" />
  </div>
</template>

<script>
import taskbar from "./components/taskbar";
import startMenu from "./components/startmenu";
import window from "./components/window";
import  {bus} from "./main";
import icons from "./components/icons"

export default {
  name: "App",
  components: {
    taskbar,
    startMenu,
    window,
    icons,
  },
  props: [],
  data() {
    return {
      windows: [],
      div: "",
      is: false,
      isminimize: [false, false, false, false, false],
    };
  },
  methods: {
    onClickTaskBarItem: function (itemName) {
      console.log(itemName , this.windows);
      if (this.isminimize[itemName]) {
        console.log("IS minimiz e= True", itemName);
        bus.$emit("open", itemName);
      } else {
        if (!getWindowObjectByID(this.windows, itemName)) {
          this.windows.push({ window, id: itemName });
         
        } else {
          console.warn("Id get Dublicated But It Throw");
          removeDublicateObjectByid(this.windows, itemName);
          this.windows.push({ window, id: itemName });
          console.log(this.windows);
        }
      }
    },
    onminimizeone: function (id) {
      this.isminimize[id] = !this.isminimize[id];
      console.log("" + id + "minimized", this.isminimize);
    },
    onStartMenu: function () {
      console.log("On Start menu Click");
    },
  },
  mounted() {
    console.log(bus)
    bus.$on("closewindow", (id) => {
      console.log("Trigger by windows close",id);
      this.isminimize[id] = false;
      removeDublicateObjectByid(this.windows, id);
      console.log("after slice window", this.windows);
    });
   },
};

function getWindowObjectByID(arr, id) {
  console.log("Calling getWindowsObjectByid");
  for (var i = 0; i < arr.length; i++) {
    console.log("getWindowsBojectBiid",arr[i].id, "log id" + id);
    if (arr[i].id == id) {
      return true;
    } else {
      return false;
    }
  }
}
// 2020/09/18 5:37 AnuradheDilshan
function removeDublicateObjectByid(arr, id) {
  for (var i = 0; i < arr.length; i++) {
    console.log(arr[i].id, "log id" + id);
    if (arr[i].id == id) {
      console.warn(arr);
      arr.splice(id, 1);
      console.warn("after reome",arr);
      //  commit By ID
    }
  }
}


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
.open {
  animation: openDrawer 0.3s;
  animation-fill-mode: forwards;
}

@keyframes openDrawer {
  from {
    display: none;
    height: 0;
  }
  to {
    display: block;
    height: 100vh;
    min-height: 250px;
  }
}
</style>
