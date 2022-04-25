<template>
  <div @click="fire" :class="color + ' filter-item'" :style="`background-image : url(${imgUrl})`">
      <slot></slot>
      </div> 

</template>

<script>
export default {
    props: {
        imgUrl : String,
        color : String,
    },
    methods: {
      fire(){
        this.emitter.emit('wearColor', this.color)
      }
    }
}
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color : black;
  font-weight: bold;
  background-size: cover;
  background-position : center;
}
</style>