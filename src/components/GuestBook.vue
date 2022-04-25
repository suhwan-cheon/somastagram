<template>
<div class="guest">
  <div class="guest-header">
    <span class="profile-name">{{guest.name}}</span>
  </div>
  <div class="guest-content">
    <div class="content"></div>
    <span class="profile-content">{{guest.content}}</span>
  </div>
</div>
</template>

<script>
export default {
  props: {
    guest : Object,
  },

}
</script>

<style>
.guest {
  padding: 0px 10px 10px 0px;
  border-color: #E7E6E6;
  box-shadow: 1.5px 1.5px 1.5px lightgray;
  border: groove;
  border-radius: 10px;
  margin: 5px 10px 5px 10px;
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
</style>