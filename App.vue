<template>
  <view class="container">
    <StatusBar/>
    <Header title="Calorie Tracker"/>
    <text class="textColorPrimary">What did you eat today?</text>
    <view class="inputContainer">
      <text-input v-model="newFood" class="input"/>
    </view>
    <touchable-opacity class="addButton" :on-press="addFood">
      <text class="buttonText">Add</text>
    </touchable-opacity>
    <text class="textColorPrimary" v-if="isValidated">Input form cannot be empty</text>
    <view class="foodList" v-for="food in foods" :key="food.id">
      <text class="textColorPrimary">{{food.name}}</text>
    </view>
  </view>
</template>

<script>
import StatusBar from "./components/StatusBar";
import Header from "./components/Header";
export default {
  data(){
    return{
      newFood: "",
      shouldValidate: false,
      foods : []
    }
  },
  components: {
    StatusBar,
    Header
  },
  methods: {
    addFood(){
      let newFood ={
        id: this.foods.length,
        name: this.newFood
      }
      this.shouldValidate = !this.newFood;
      if(!this.shouldValidate)
        this.foods.push(newFood);
      this.newFood = '';
    }
  },
  computed:{
    isValidated(){
      return !this.newFood && this.shouldValidate
    }
  }
}
</script>

<style>
.container {
  background-color: #252525;
  flex: 1;
}
.textColorPrimary{
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
.addButton{
  background-color: #AAAAAA;
  width: 10%;
  align-self: center;
}
.buttonText{
  font-size: 18px;
  font-weight: 300;
  text-align: center;
}
</style>
