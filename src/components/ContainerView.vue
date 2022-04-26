<template>
  <!-- 게시글 -->
  <div v-if="step == 0">
  <PostView :post="post" v-for="(post) in posts" :key="post" />
  </div>  
  <!-- 필터선택페이지 -->
  <div v-if="step == 1">
    <div :class="filterName + ' upload-image'" :style="{backgroundImage : `url(${imgUrl})`}"></div>
    <div class="filters">
      <FilterBox :imgUrl="imgUrl" :color="color" v-for="color in colors" :key="color">
        {{ color }}
      </FilterBox>
    </div>
  </div>

  <!-- 글작성페이지 -->
  <div v-if="step == 2">
    <div :class="filterName + ' upload-image'" :style="{backgroundImage : `url(${imgUrl})`}"></div>
    <div class="write">
      <textarea class="write-box" @input="$emit('write', $event.target.value)">write!</textarea>
    </div>
  </div>

  <!-- 방명록 페이지 -->
  <div v-if="step == 3">
    <div class="guest-total">
      <h4 class="guestHeader">방명록</h4>
      <div class="guest-comment">
        <GuestBook :guest="guest" v-for="(guest) in guests" :key="guest"/>
      </div>
      <div class="guest-input">
        <div class="guest-box">
          <input class = "input-box" placeholder="닉네임" @input="$emit('nickName', $event.target.value)">
        </div>
        <div class="write-guest">
          <textarea class="write-box" placeholder="방명록을 남겨주세요 :D" @input="$emit('guestContext', $event.target.value)"></textarea>
        </div>
      </div>
    </div>
    <div class="footer-button-plus" style="margin-bottom: 5px;"> 
      <span class="input-plus" @click="$emit('add')">작성</span>
    </div>
  </div>
</template>

<script>
import PostView from './PostView.vue'
import FilterBox from './FilterBox.vue'
import colorData from '../assets/colordata.js'
import GuestBook from './GuestBook.vue'

export default {
  data() {
    return {
      colors : colorData,
    }
  },
  components: {
    PostView,
    FilterBox,
    GuestBook,
  },
  props: {
    posts : Array,
    step : Number,
    imgUrl : String,
    message : String,
    filterName : String,
    guests : Array,
  },
  methods: {
  }
}
</script>

<style>
.guestHeader {
  padding-left: 20px;
  margin: 10px 10px 10px 10px;
}
.guest-total{
  position:relative; 
  padding-top: 10px;
  margin: 15px 20px 15px 20px;
  color: #000; 
  border-radius: 10px; 
  background-color: #E6E6E6;
}
.guest-comment{
  background-color: #FFF;
  padding: 30px 0px 30px 0px;
}

.guest-box h5 {
  margin: 0px 0px 4px 10px;
}
.input-box{
  font-size: 15px;
  border: 0;
  outline: none;
  padding-left: 10px;
}
.guest-input{
  position:relative; 
  margin: 15px 20px 15px 20px;
  padding: 0px 10px 10px 0px;
  color: #000; 
  border-radius: 10px; 
}

.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
.guest-box {
  padding: 15px;
  margin: auto;
}
</style>