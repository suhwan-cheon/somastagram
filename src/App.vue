<template>
  <div class="header">
    <ul class="header-button-left">
      <li v-if="step != 0" @click="step = 0" >Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 0" @click="step = 3">방명록</li>
      <li v-if="step == 1" @click="step++">Next</li>
      <li v-if="step == 2" @click="publish">발행</li>
    </ul>
    <img src="./assets/movie.png" class="logo" />
  </div>

  <ContainerView :filterName="filterName" :guests="guests" :posts="posts" :step="step" :imgUrl="imgUrl" v-on:write="message = $event"/>

  <div v-if="step == 0" class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">글 작성</label>
    </ul>
 </div>
 
</template>

<script>
import ContainerView from './components/ContainerView.vue'
import postdatas from './assets/postdata.js'
import guestdatas from './assets/guestdata.js'
import { mapMutations, mapState } from 'vuex'

export default {

  name: 'App',
  data() {
    return {
      posts: postdatas,
      guests: guestdatas,
      clicks : 0,
      url : '',
      step : 0,
      imgUrl : '',
      message : '',
      filterName : '',
    }
  },
  mounted() {
    this.emitter.on('wearColor', (color)=> {
      this.filterName = color;
    })
  },
  components: {
    ContainerView,
  },
  methods: {

    ...mapMutations(['setMore']),
     upload(e){
       let file = e.target.files;
       this.imgUrl = URL.createObjectURL(file[0]);
       this.step = 1;
     },
     publish(){
       var myPost = {
          name: "소마 13기",
          userImage: "https://placeimg.com/100/100/arch",
          postImage: this.imgUrl,
          likes: 0,
          date: "Apr 25",
          liked: false,
          content: this.message,
          filter: this.filterName,
       };
       this.posts.unshift(myPost);
       this.step = 0;
     },
  },

  // computed 함수는 항상 return이 있어야 한다.
  computed : {
    name(){
      return this.$store.state.name;
    },
    ...mapState(['name', 'age', 'likes']),
    ...mapState({ othername : 'name'})

  }
}
</script>

<style>

body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
  z-index: 100;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 15px;
  font-style: bold;
  padding-top: 12px;
}
.footer-button-plus:hover {
  opacity: 0.5;
  filter: alpha(opacity=50);
  color: #4ba2db;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
