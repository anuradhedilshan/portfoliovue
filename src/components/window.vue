<template>

  <div class="window_box" data-x="0" data-y="0" id="window_box" v-if="is">
    <div class="actionBar">
      
      <img src="../assets/From Templates/close.png" @click="is= !is" id="close" />
      <img src="../assets/From Templates/minimize.png" id="minimize" />
      <img src="../assets/From Templates/screen.png" id="screen" />
    </div>
    <div id="window_holder">

<button id="lk"  @click="addElem"> CLick vue </button>

    </div>

  </div>
  
</template>
<script>
import interact from "interactjs";



export default {
  name: "window",
  methods: {
addElem: function () {
console.log("klklk");
  
}

  },
  data() {
    return {
      is: true,
    };
  },
  computed: {
    close: function () {
  
       return this.is;
    },
  },

  mounted() {
    resizeanddrag();
  },
};

function resizeanddrag() {
  interact(".window_box")
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
</script>
<style scoped>
template {
  overflow: hidden;
  padding: 100px;
}
.window_box {
  position: relative;
  width: 800px;
  height: 50vh;
  background: rgba(24, 9, 49, 0.8);
 
  left: 0;
  touch-action: auto;
  box-sizing: border-box;
  overflow: auto;
  top: 10px;
  touch-action: none;
  user-select: none;
  z-index: 112;
  box-shadow:white 0 10px 10px -5px;
}
.window_box::before {
  content: none;
}
#window_holder {
  width: 100%;
   padding: 5px;
}
.window_box .actionBar {
  width: 100%;
  padding: 2px;
  border-radius:2px;
   background:black;
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