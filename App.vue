<template>
  <view class="container">
    <StatusBar/>
    <Header title="Calorie Tracker"/>
    <text class="text-color-primary">What did you eat today?</text>
    <view class="inputContainer">
      <text-input v-model="newFood" class="input"/>
    </view>
  </view>
</template>

<script>
import StatusBar from "./components/StatusBar";
import Header from "./components/Header";
export default {
  data(){
    return{
      newFood: ""
    }
  },
  components: {
    StatusBar,
    Header
  }
}
</script>

<style>
.container {
  background-color: #252525;
  flex: 1;
}
.text-color-primary{
  font-size: 24px;
  margin-top: 20px;
  color: #AAAAAA;
  text-align: center;
}
.inputContainer{
  margin-top: 20px;
  flex-direction: row;
  justify-content: center;
}
.input{
  background-color: ghostwhite;
  flex: 1;
  border-color: black;
  font-size: 20px;
  font-weight: 300;
}
</style>
