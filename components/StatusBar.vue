<!--Component is only shown in mobile version-->
<!--Replaces the standard iOS status bar with a black one-->
<template>
  <view class="statusbar"></view>
</template>

<script>
export default {
  name: "StatusBar"
}
</script>

<style>
.statusbar{
  height: 20px;
  background-color: #000000;
}
</style>