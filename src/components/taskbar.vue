<template>
        <!-- Task Bar start -->
    <div class="taskbar-bottom">
      <ul class="menu">
        <li style="float: left;">
          <img src="../assets/From Templates/Menu.png" style="transform: scale(0.8);" />
        </li>
      </ul>
      <div class="social_bar">
        <ul>
          <li class="activeWindow">
            
            <img @click="$emit('onclicktaskbar','facebook')" src="../assets/From Templates/Facebook.png" style="transform: scale(0.7);" />
             
          </li>
          <li>
            <img src="../assets/From Templates/whatsapp.png" style="transform: scale(0.7);" />
          </li>
          <li>
            <img src="../assets/From Templates/linked.png" style="transform: scale(0.9);" />
          </li>
          <li>
            <img src="../assets/From Templates/Github.png" style="transform: scale(0.8);" />
          </li>
          <li>
            <img src="../assets/From Templates/G-mail.png" style="transform: scale(0.8);" />
          </li>
        </ul>
      </div>
      <ul class="help">
        <li style="float: right;">
          <img src="../assets/From Templates/Help.png" style="transform: scale(0.7);" />
        </li>
        <li class="noR" style="margin-top: 10px;">
          ENG
        </li>
        <li class="noR" style="margin-top: 10px;">
          2:45 PM
        </li>
      </ul>
    </div>
    <!-- end Task Bar -->
</template>

<script>
export default {
    name: "task bar",
   
  




}
</script>
<style scoped>

/* Task Bar */
.taskbar-bottom {
  width: 100%;
  position: fixed;
  left: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-self: center;
  align-items: center;
  color: white;
  background-color: #00000075;
}

.taskbar-bottom ul {
  margin: auto;
}

.taskbar-bottom ul li {
  display: inline-block;
  padding: 3px;
  opacity: 0.93;
  margin: auto;
  vertical-align: middle;
  text-align: center;
}

.taskbar-bottom ul li:hover {
  opacity: 1;
  background: #00000090;
  filter: brightness(150%)
}

.taskbar-bottom ul.menu {
  flex: auto;
}

.taskbar-bottom ul.social_bar {
  flex: auto;
  flex-shrink: inherit;
}

.activeWindow:before {
  content: "";
  width: 46px;
  height: 5px;
  transform: translate(-3.4px, -5px);
  background-color: #1dffd993;
  position: absolute;
}

.taskbar-bottom ul.help {
  flex: auto;
  align-self: flex-end;
}

.taskbar-bottom ul.help li {
  float: right;
}

.taskbar-bottom li img {
  width: 40px;
}

/* Task Bar end */
@media (max-width:440px) {

  /* Task Bar */
  .taskbar-bottom ul.help li.noR {
    display: none;
  }

  /* Task Bar end */
}
</style>