<template>
  <view class="header">
    <text class="title">{{title}}</text>
  </view>
</template>

<script>
export default {
  name: "Header",
  props: ['title']
}
</script>

<style>
.header{
  height: 60px;
  background-color: black;
  align-items: center;
  justify-content: center;
}
.title{
  font-size: 28px;
  font-weight: 500;
  color: ghostwhite;
}
</style>