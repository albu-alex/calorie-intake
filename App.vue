<template>
  <view class="container">
    <StatusBar/>
    <Header title="Calorie Tracker"/>
    <text class="textColorPrimary">What did you eat today?</text>
    <text class="textColorPrimary" v-if="isValidated">Input form cannot be empty</text>
    <view class="inputContainer">
      <text-input v-model="newFood" class="input"/>
    </view>
    <touchable-opacity class="addButton" :on-press="addFood">
      <text class="buttonText">Add</text>
    </touchable-opacity>
    <view class="foodList" v-for="food in foods" :key="food.id">
      <text class="foodListItem">{{food.name}}</text>
      <text-input v-if="foods.length-1 === food.id" v-model="newQuantity" class="quantityInput"/>
      <touchable-opacity :on-press="() => addQuantity(food.id)" class="addQuantityButton">
        <text class="quantityButton">Add Quantity</text>
      </touchable-opacity>
    </view>
    <text class="textColorPrimary" v-if="countCalories">You have eaten this many calories:{{calorieCounter}}</text>
    <touchable-opacity class="resetButton" :on-press="resetFoodList">
      <Footer/>
    </touchable-opacity>
  </view>
</template>

<script>
import StatusBar from "./components/StatusBar";
import Header from "./components/Header";
import Footer from "./components/Footer";
export default {
  data(){
    return{
      newQuantity: "0",
      newFood: "",
      shouldValidate: false,
      isEmpty: true,
      foods : [],
      calorieCounter : 0,
      caloriesPerFood:{
        "Chicken breast" : 1.64,
        "Chocolate": 5,
        "Yoghurt": 0.58,
        "Milk": 0.42,
        "Bread": 2.64,
        "Rice": 1.3,
        "Eggs": 1.55
      }
    }
  },
  components: {
    StatusBar,
    Header,
    Footer
  },
  methods: {
    addQuantity(index){
      this.foods[index].quantity = parseInt(this.newQuantity);
    },
    resetFoodList(){
      this.foods = [];
      this.newQuantity = "0";
      this.calorieCounter = 0;
    },
    addFood(){
      let newFood ={
        id: this.foods.length,
        name: this.newFood,
        quantity: 0
      }
      if(!(this.newFood in this.caloriesPerFood))
        return;
      this.shouldValidate = !this.newFood;
      if(!this.shouldValidate)
        this.foods.push(newFood);
      this.newQuantity = "0";
      this.newFood = '';
    }
  },
  computed:{
    countCalories(){
      if(this.foods.length === 0)
        return 0;
      this.calorieCounter += this.foods[this.foods.length-1].quantity * this.caloriesPerFood[this.foods[this.foods.length-1].name];
      return this.calorieCounter;
    },
    isValidated(){
      return !this.newFood && this.shouldValidate
    }
  }
}
</script>

<style>
.addQuantityButton{
  margin-top: 20px;
}
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
  align-self: flex-end;
}
.input{
  background-color: ghostwhite;
  flex: 1;
  border-color: black;
  font-size: 20px;
  font-weight: 300;
}
.quantityInput{
  margin-top: 20px;
  background-color: #252525;
  color: #AAAAAA;
  border-color: black;
  font-size: 16px;
  font-weight: 600;
  max-width: 200px;
  min-width: 50px;
}
.addButton{
  background-color: #AAAAAA;
  width: 10%;
  align-self: center;
}
.resetButton{
  position: absolute;
  top: 87%;
  width: 100%;
}
.quantityButton{
  font-size: 18px;
  font-weight: 300;
  text-align: center;
  color: #AAAAAA;
}
.buttonText{
  font-size: 18px;
  font-weight: 300;
  text-align: center;
}
.foodListItem{
  font-size: 24px;
  font-weight: 300;
  margin-top: 20px;
  color: #AAAAAA;
  text-align: justify;
  margin-left: 2%;
}
.foodList{
  line-height: 50px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
