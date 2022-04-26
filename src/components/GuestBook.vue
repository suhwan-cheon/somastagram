<template>
<div class="profile" :style="{ backgroundImage : `url('https://randomuser.me/api/portraits/men/${this.num}.jpg')`}"></div>

<div class="guest">
  <div class="guest-header">
    <span class="profile-name">{{guest.name}}</span>
  </div>
  <div class="guest-content">
    <div class="content"></div>
    <span class="profile-content"><pre class="propre">{{guest.content}}</pre></span>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      num: Math.ceil(Math.random()*10),
    }
  },
  props: {
    guest : Object,
  },

}
</script>

<style>
.guest{
  position:relative; 
  margin: 15px 20px 15px 70px;
  padding: 0px 10px 10px 0px;
  color: #000; 
  border-radius: 10px; 
  background-color: #E8E8E8;
  }

.guest-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.guest:after {
 border-top:15px solid #E8E8E8; 
 border-left: 15px solid transparent;
 border-right: 0px solid transparent;
 border-bottom: 0px solid transparent;
 content:"";
 position:absolute;
 top:10px;
 left:-15px;
}
.profile-name {
  font-weight: bold;
}
.guest-header {
  height: 30px;
  padding: 5px;
}
.guest-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.profile {
  
  width: 30px;
  height: 30px;
  margin: 0px 0px 0px 20px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
  background-color: #E8E8E8;
}
.propre {
  margin : 0;
}
</style>