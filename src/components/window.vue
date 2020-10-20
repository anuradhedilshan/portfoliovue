<template  >
  <div
    v-bind:class="[classd, window_box_Id]"
    class="window_box"
    data-x="0"
    data-y="0"
    id="window_box"
    v-if="is"
  >
    <div class="actionBar">
      <img
        src="../assets/From Templates/close.png"
        @click="close()"
        id="close"
      />
      <img
        src="../assets/From Templates/minimize.png"
        @click="minimize"
        id="minimize"
      />
      <img
        src="../assets/From Templates/screen.png"
        @click="screen()"
        id="screen"
      />
    </div>

    <div :id="holder_Id" class="window_holder">
      <!-- Placeholder -->
    </div>
  </div>
</template>

<script>
import interact from "interactjs";
import { bus } from "../main";

export default {
  name: "window",
  methods: {
    close: function () {
      this.is = false;

      try {
        //  document.body.removeChild(script);
      } catch (e) {
        console.error(e);
      }
      bus.$emit("closewindow", this.id);
    },
    minimize: function () {
      this.$emit("minimizeone", this.id);
      this.isminimize = true;
    },
    screen: function (v) {
      var ld = document.getElementById("window_box");

      ld.style.width = 100 + "%";
      ld.style.height = 100 + "%";
      console.log(ld.className);
      console.log(v);
    },
  },
  data() {
    return {
      is: true,
      classd: "",
      isminimize: false,
      window_box_Id: "windowBox_id" + this.id,
      holder_Id: "holder_id" + this.id,
    };
  },
  props: ["id"],
  mounted() {
    console.warn("Mounted Windoes ");
    resizeanddrag(this.window_box_Id);
    bus.$on("open", (id) => {
      console.log("trigger Open", id, this.id);
      if (id == this.id) {
        this.isminimize = false;
      }
    });
    // var data = getRoutorRawData();
    setRawData(this.id,this.holder_Id);

  },
  watch: {
    isminimize: function (val) {
      this.classd = val == true ? "minimize" : "oncurrent";
      console.log("Value Change", val);
    },
  },
};

function resizeanddrag(window_box_clas) {
  interact("."+window_box_clas)
    .draggable({
      modifiers: [
        interact.modifiers.restrict({
          restriction: "parent",
          endOnly: true,
        }),
      ],
      autoScroll: false,
      listeners: {
        move(event) {
          var target = event.target;
          // keep the dragged position in the data-x/data-y attributes
          var x = (parseFloat(target.getAttribute("data-x")) || 0) + event.dx;
          var y = (parseFloat(target.getAttribute("data-y")) || 0) + event.dy;

          // translate the element
          target.style.webkitTransform = target.style.transform =
            "translate(" + x + "px, " + y + "px)";

          // update the posiion attributes
          target.setAttribute("data-x", x);
          target.setAttribute("data-y", y);
        },
      },
    })
    .resizable({
      // resize from all edges and corners
      edges: { left: true, right: true, bottom: true, top: true },

      listeners: {
        move(event) {
          var target = event.target;
          var x = parseFloat(target.getAttribute("data-x")) || 0;
          var y = parseFloat(target.getAttribute("data-y")) || 0;

          // update the element's style
          target.style.width = event.rect.width + "px";
          target.style.height = event.rect.height + "px";

          // translate when resizing from top or left edges
          x += event.deltaRect.left;
          y += event.deltaRect.top;

          target.style.webkitTransform = target.style.transform =
            "translate(" + x + "px," + y + "px)";

          target.setAttribute("data-x", x);
          target.setAttribute("data-y", y);
        },
      },
      modifiers: [
        // keep the edges inside the parent
        interact.modifiers.restrict({
          outer: "parent",
        }),

        // minimum size
        interact.modifiers.restrictSize({
          min: { width: 100, height: 50 },
        }),
      ],

      inertia: true,
    });
}
var root = document.getElementsByTagName("template");
console.log(root);
async function setRawData(id,window_holder_id) {
  var data = fetch("./routor.json");
  var routeG = null;
  var pluginG = null;
  await data
    .then((responce) => {
      return responce.json();
    })
    .then((data) => {
      var Rdata = data[id];
      var plugin = Rdata["plugin"];
      var route = Rdata["route"];
      console.log("SETRAW DATA PLUG AND ROUTE", plugin, route);
      // add Pluging to dom
      routeG = route;
      pluginG = plugin;
      var xhttp = new XMLHttpRequest();
      xhttp.onreadystatechange = function () {
        if (this.readyState == 4 && this.status == 200) {
  console.log("ELEMENT IS", document.getElementById(window_holder_id),"id = "+ window_holder_id)
          document.getElementById(window_holder_id).innerHTML = this.response;
          if (pluginG != "") {
            var script = document.createElement("script");
            script.setAttribute("src", pluginG);
            document.body.appendChild(script);

            setTimeout(() => {
              document.body.removeChild(script);
            }, 10000);
          }
        }
      };
      xhttp.open("GET", routeG, false);
      xhttp.send(null);
    })
    .catch((error) => {
      console.error("Cannot Get value from .routorJson" + error);
      return null;
    });
  console.log("after pass data ");

  console.log(pluginG);
}

// function getRoutorRawData() {
//   var xhttp = new XMLHttpRequest();
//   xhttp.onreadystatechange = function () {
//     if (this.readyState == 4 && this.status == 200) {
//       var jsonObject = JSON.parse(this.response);
//       console.log(jsonObject);
//       return jsonObject;
//     } else {
//       return null;
//     }
//   };
//   xhttp.open("GET", "./routor.json", true);
//   xhttp.send(null);
// }
</script>
<style scoped>
template {
  overflow: hidden;
  padding: 100px;
  background: green;
}

.minimize {
  animation: minimizing 1s;
  animation-fill-mode: forwards;
}
.oncurrent {
  display: block;
  transform: translateY(0);
}
@keyframes minimizing {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(300%);
    display: none;
  }
}

.window_box {
  width: 100%;
  height: 100%;
  background: rgba(24, 9, 49, 0.8);
  left: 0;
  box-sizing: border-box;
  padding-bottom: 20px;
  position: relative;
  object-fit: cover;
  touch-action: auto;
  top: 10px;
  touch-action: none;
  user-select: none;
  z-index: 112;
  box-shadow: white 0 10px 10px -5px;
  -ms-overflow-style: none; /* Internet Explorer 10+ */
  scrollbar-width: none; /* Firefox */
}
div.window_box ::-webkit-scrollbar {
  display: none;
}
.window_box::before {
  content: none;
}
.window_holder {
  position: relative;
  margin: auto;
  width: 100%;
  max-height: 100vh;
  height: 100%;
  padding: 5px;
  overflow: auto;
}
.window_box .actionBar {
  width: 100%;
  padding: 2px;
  position: sticky;
  border-radius: 2px;
  background: black;
  overflow: auto;
}
.window_box .actionBar img {
  padding: 4px;
  float: right;
  cursor: pointer;
}
.window_box .actionBar #minimize {
}
.window_box .actionBar #screen {
}
.window_box .actionBar #close {
}

.window_box .actionBar img:hover {
  background: #00000090;
  filter: brightness(150%);
}
</style>