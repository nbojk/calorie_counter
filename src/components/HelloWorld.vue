<template>
  <div class="hello">
    <h1>Vue.js Calorie Counter</h1>
    <div id="titles">
      <span>description </span>
      <span>calories</span>
      <span>fat</span>
      <span>carbs</span>
      <span>protein</span>
    </div>
    
    <ul>
      <li v-for="(item, index) in listOfItems" v-bind:key="index">
        <span>{{item.name}}</span>
        <span>{{item.calories}}</span>
        <span>{{item.carbs}}</span>
        <span>{{item.fat}}</span>
        <span>{{item.prot}}</span>
        &nbsp; 
        <button v-on:click="removeItem(index)">&#10060;</button> 
        
      </li> 
    </ul>

    <div id="totals">
      <span>Totals:</span>
      <span>{{totals.totalCal}}</span>
      <span>{{totals.totalCarbs}}</span>
      <span>{{totals.totalFat}}</span>
      <span>{{totals.totalProt}}</span>
    </div>

    <div id="newItem">
      <input v-bind:placeholder="placeholderValues.inputNameText" v-model="newValues.newName" type="text">
      <input v-bind:placeholder="placeholderValues.inputCalorieText" v-model="newValues.newCalories" type="number">
      <input v-bind:placeholder="placeholderValues.inputCarbsText" v-model="newValues.newCarbs" type="number">
      <input v-bind:placeholder="placeholderValues.inputFatText" v-model="newValues.newFat" type="number">
      <input v-bind:placeholder="placeholderValues.inputProteinText" v-model="newValues.newProtein" type="number">
      <button v-on:click="addItem">+</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function(){
    return {
      placeholderValues:{
        inputNameText:'Description',
        inputCalorieText:'Calories',
        inputCarbsText:'Fat',
        inputFatText:'Carbs',
        inputProteinText:'Protein'
        },
      newValues:{
        newName:'',
        newCalories:'',
        newCarbs:'',
        newFat:'',
        newProtein:''
      },
      listOfItems: [
          {
          name:'This is an item',
          calories: 223,
          carbs: 12,
          fat: 30,
          prot: 10
        },
        {
          name:'This is also an item',
          calories: 50,
          carbs: 1,
          fat: 10,
          prot: 1
        },
        {
          name:'Hey, me, too!',
          calories: 175,
          carbs: 3,
          fat: 15,
          prot: 8
        }
      ],
      totals: {
        totalCal: 448,
        totalCarbs: 16,
        totalFat: 55,
        totalProt: 19
      }
    }
  },
  methods: {
    addItem: function(){
      this.listOfItems.push({
        name: this.newValues.newName,
        calories: this.newValues.newCalories,
        carbs: this.newValues.newCarbs,
        fat: this.newValues.newFat,
        prot: this.newValues.newProtein,
      });
      this.newValues.newName = null,      
      this.newValues.newCalories = null,  
      this.newValues.newCarbs = null,
      this.newValues.newFat = null,
      this.newValues.newProtein = null,
      this.calcValues()
    },
    removeItem: function(itemIndex){ 
    this.listOfItems.splice(itemIndex,1); 
    this.calcValues()
    },
    calcValues: function(){
      
        this.totals.totalCal = 0;
        this.totals.totalCarbs = 0;
        this.totals.totalFat = 0;
        this.totals.totalProt = 0;
      for(let i = 0; i < this.listOfItems.length; i++){ 
       
        this.totals.totalCal += parseInt(this.listOfItems[i].calories); 
        this.totals.totalCarbs += parseInt(this.listOfItems[i].carbs);
        this.totals.totalFat += parseInt(this.listOfItems[i].fat);
        this.totals.totalProt += parseInt(this.listOfItems[i].prot);
      }
    }
  }
}
</script>


<style scoped lang='scss'>
  .hello {
    min-width:680px;
    max-width:850px;
    width:70%;
    margin: 0 auto;
    border:1px solid #333;
    position: relative; 
    font-family: 'Helvetica';
    border-radius: 10px;
    h1{
      background-color:rgb(70, 161, 131);
      color: #fff;
      margin:0;
      padding:20px 0;
      text-align: center;
      border-top-left-radius: 9px;
      border-top-right-radius: 9px;
      background-image: url('../assets/cardio.svg');
      background-size:100px;
      background-repeat: no-repeat;
      background-position: 15px -10px;
    }
    #titles {
      text-transform: uppercase;
      display:flex;
      justify-content: space-between;
      padding:14px 15px;
      border-bottom:1px solid gray;
      font-weight: bold;
      span {
        display: inline-block;
        width: 100px;
        padding: 5px 5px 5px 5px;
        &:nth-child(1){
          width:25%;
        }
      }
    }
    ul {
      padding: 0;
      margin: 0;
      padding: 20px 34px;
      li{
        list-style-type: none;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: space-between;
        position: relative;
        padding-top: 5px;
        span {
          display: inline-block;
          width: 100px;
          padding: 5px 0 2px 5px;
          border-bottom: 1px solid gray;
          &:nth-child(1){
            width:25%;
          }
        }
        button {
          position: absolute;
          right: -32px;
          bottom: 0px;
          color: red;
          background-color: rgba(0,0,0,0);
          font-size: 20px;
          border: none;
          transition: 0.3s transform;
          &:hover {
            cursor: pointer;
            transform: scale(1.5);
          }
        }
      }
    }
    #totals {
      display: flex;
      justify-content: space-between;
      background-color: lightgray;
      padding:20px 24px;
      span {
        display: inline-block;
        padding-left: 5px;
        width: 100px;
        font-weight: bold;
        font-size: 20px;
        &:nth-child(1){
          width: 25%;
          font-weight: normal;
        }
      }
    }
    #newItem {
      display: flex;
      justify-content: space-between;
      padding: 20px 20px 30px;
      input {
        border: none;
        border-bottom: 1px solid #333;
        width: 100px;
        padding: 5px 0 5px 10px;
        display: inline-block;
        &:nth-child(1){
            width: 25%;
          }
        &:focus {
          outline: none;
        }
      }
      button {
        position: absolute;
        right: -22px;
        bottom:-22px;
        border-radius: 50%;
        background-color: rgb(70, 161, 131);
        width: 60px;
        height: 60px;
        color: #fff;
        font-size: 30px;
        border: none;
        &:hover {
          background-color: rgb(93, 218, 176);
          cursor: pointer;
        }
      }
    }
  }
</style>

