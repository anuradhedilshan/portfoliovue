<template>
  <!-- StartMenu star -->
  <div   class=" start_menu_box row mb-2 " style="width: 100%;">
    <div class="start_menu col-11 col-md-5 col-lg-5 col-sm-11 bg-dark">
      <div class="col-7 float-left">
        <ul class="fav-applications" style="list-style: none;">
          <li>
            <h6>Fav Applications</h6>
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\androidStudio.png" />
            Android Studio
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\chrome.png" />
            Google Chorme
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\opera.png" />
            Opera Mini
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\pycharm.png" />
            Py Charm
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\sublime_text.png" />
            Sublime Text
          </li>
          <li>
            <img src="..\assets\From Templates\fav_applications\vs-code.png" />
            VS-Code
          </li>
        </ul>

        <div class="updates">
          <h6 style="color: white;">Updates</h6>

          <img src="https://picsum.photos/260/237" alt />
        </div>

        <ul class="power_options">
          <li>
            <h6>Power Options</h6>
          </li>
          <li class="power_option_item">
            <img
              style="transform:scale(1.3) translateY(-4px);"
              src="https://img.icons8.com/cotton/64/000000/rating.png"
            />
            Rate my work
          </li>
          <li class="power_option_item">
            <img src="https://img.icons8.com/cute-clipart/64/000000/share.png" />
            Share
          </li>
          <li class="power_option_item">
            <img src="https://img.icons8.com/cotton/64/000000/power-off-button.png" />Power
          </li>
        </ul>
      </div>

      <div class="col-5 float-right mt-2 mb-2 blogBox">
        <ul class="blog" style="list-style: none;">
          <li style="padding: 2px; color: white;">
            <h6>My Blog</h6>
          </li>

          <li class="blog_item">
            <img src="../assets/From Templates/whatsapp.png" alt />
            <span>hello world hello worldhello .......Read more</span>
          </li>
          <li class="blog_item">
            <img src="https://picsum.photos/137/137" alt />
            <span>hello world hello worldhello .......Read more</span>
          </li>
          <li class="blog_item">
            <img src="https://picsum.photos/137/137" alt />
            <span>hello world hello worldhello .......Read more</span>
          </li>
          <li class="blog_item">
            <img src="https://picsum.photos/137/137" alt />
            <span>hello world hello worldhello .......Read more</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
  <!-- StartMenu End -->
</template>

<script>
export default {
  name: "startMenu",
  data() {
    return {
      is: false,
      holder_class: "open"
    };
  },
  methods:{
    onStartMenu: function (){
      console.log("On Start menu Click");
      this.is = ! this.is;
    }
  },

  
};
</script>

<style scoped>
/* StartMenu */
.start_menu_box {
  
  padding-top: 50px;
  height: 0;
  display: block;
  position: absolute;
  z-index: 100;
  left: 0;
  bottom: 45px;
  overflow: auto;

}


.start_menu::-webkit-scrollbar {
  width: 5px;
}

/* Track */
.start_menu::-webkit-scrollbar-track {
  background: #f1f1f1;
  width: 5px;
}

/* Handle */
.start_menu::-webkit-scrollbar-thumb {
  background: #888;
  width: 5px;
}

/* Handle on hover */
.start_menu::-webkit-scrollbar-thumb:hover {
  background: #555;
}

.start_menu {
  overflow: auto;
  position: relative;
  scrollbar-width: thin;
  height: 100%;
  background: red;
}

.start_menu .fav-applications {
  border: var(--start_menu_border);
  padding: 5px;
  margin-top: 10px;
}

.start_menu .fav-applications li {
  padding: 3px;
  color: white;
  text-align: justify;
  position: relative;
  margin-top: 2px;
  padding: 5px;
  filter: brightness(70%);
  font-size: 13px;
  transition: filter 0.5s linear;
}

.start_menu .fav-applications li:hover {
  filter: brightness(150%);
  background: #00000090;
}

.start_menu .fav-applications li img {
  width: 33px;
  height: 32px;
  margin-left: 10px;
}

.start_menu .blogBox {
  border: var(--start_menu_border);
}

.start_menu .blog li.blog_item {
  padding: 2px;
  overflow: hidden;
  padding: 5px;
  margin-top: 5px;
  border: 0.5px solid black;
}

.start_menu .blog .blog_item img {
  height: 160px;
  width: 100%;
  filter: grayscale(20%);
}

.start_menu .blog .blog_item:hover {
  border: 1px solid yellow;
}

.start_menu .blog .blog_item span {
  color: white;
  position: absolute;
  padding: 5px;
  background: rgba(0, 0, 0, 0.123);
  z-index: 101;
  transform: translateY(-100px);
  display: -webkit-box;
  -webkit-line-clamp: 5;
  overflow: hidden;
  -webkit-box-orient: vertical;
}

.updates {
  border: var(--start_menu_border);
  padding: 5px;
  overflow: hidden;
}

.start_menu .power_options {
  width: 100%;
  min-height: 200px;
  list-style: none;
  margin-top: 40px;
  border: var(--start_menu_border);
}

.start_menu .power_options img {
  transform: scale(1.2);
  max-height: 22px;
  max-width: 22px;
  margin-right: 10px;
}

.power_options li {
  color: white;
  text-align: justify;
  margin-top: 5px;
  margin-left: 10px;
  padding: 5px;
}

.power_options li:hover {
  filter: brightness(150%);
  background: #00000090;
}

/* StatMenu End */
</style>