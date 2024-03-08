<script setup>
import { ref } from 'vue';

const isOpClicked = ref(false);
const firstNum = ref("");
const secondNum = ref("");
const operation = ref("none");
const result = ref(0.0);
const showError = ref(false);

function append(number){
    showError.value = false;
    if(!isOpClicked.value)
    {
      console.log("first", number)
      firstNum.value += number;
      result.value = parseFloat(firstNum.value) ;
    }
      
    else
    {
      console.log("second", number)
      secondNum.value += number;
      result.value = parseFloat(secondNum.value) ;
    }
      
    console.log(firstNum.value);
    console.log(secondNum.value);
}

function plus(){
  showError.value = false;
  isOpClicked.value = true;
  operation.value = "plus"
  result.value = 0.0;


}

function minus(){
  showError.value = false;
  isOpClicked.value = true;
  operation.value = "minus"
  result.value = 0.0;
}

function multiply(){
  showError.value = false;
  isOpClicked.value = true;
  operation.value = "multiply"
  result.value = 0.0;

}

function divide(){
  showError.value = false;
  isOpClicked.value = true;
  operation.value = "divide"
  result.value = 0.0;
  

}

function equal(){
  console.log(isOpClicked.value , firstNum.value.length>0, secondNum.value.length>0)
  if(isOpClicked.value && firstNum.value.length>0 && secondNum.value.length>0){
    console.log(firstNum, secondNum)
    let num1 = parseFloat(firstNum.value);
    let num2 = parseFloat(secondNum.value)
    console.log(operation.value)
    if (operation.value === "plus"){
      console.log(num1, num2)
      result.value = num1 + num2
      console.log("plusx", result)
    }
    if (operation.value === "minus"){
      result.value = num1 - num2
    }
    if (operation.value === "multiply"){
      result.value = num1 * num2
    }
    if (operation.value === "divide"){
      if (num2 == 0){
        console.log("Cannot divide by zero")
        showError.value = true;
        clear();
        return;
      }
      result.value = num1 / num2
    }
  }
}

function clear(){
  isOpClicked.value = false
  firstNum.value = ""
  secondNum.value = ""
  operation.value = "none"
  result.value = 0.0
}
</script>



<template>
  <html>

  <body>
    <div id="app">
      <div class="container">
        <div class="calculator">
          <div v-if="showError" class="display">Can't divide by zero</div>
          <div class="display">{{ result }}</div>
          <div @click="clear" id="clear" class="btn operator">C</div>
          <div  id="sign" class="btn operator">::</div>
          <div  id="percent" class="btn operator">
            ::
          </div>
          <div @click="divide" id="divide" class="btn operator">
            /
          </div>
          <div @click="append('7')" id="n7" class="btn">7</div>
          <div @click="append('8')" id="n8" class="btn">8</div>
          <div @click="append('9')" id="n9" class="btn">9</div>
          <div @click="multiply" id="times" class="btn operator">*</div>
          <div @click="append('4')" id="n4" class="btn">4</div>
          <div @click="append('5')" id="n5" class="btn">5</div>
          <div @click="append('6')" id="n6" class="btn">6</div>
          <div @click="minus" id="minus" class="btn operator">-</div>
          <div @click="append('1')" id="n1" class="btn">1</div>
          <div @click="append('2')" id="n2" class="btn">2</div>
          <div @click="append('3')" id="n3" class="btn">3</div>
          <div @click="plus" id="plus" class="btn operator">+</div>
          <div @click="append('0')" id="n0" class="zero">0</div>
          <div @click="append('.')" id="dot" class="btn">.</div>
          <div @click="equal" id="equal" class="btn operator">=</div>
        </div>
      </div>
    </div>
  </body>

  </html>
</template>


<style scope>
@import url("https://fonts.googleapis.com/css?family=Poppins:300,500&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

::selection {
  background: none;
}

body {
  background-color: #3ffce3;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
}

.calculator {
  display: grid;
  grid-template-rows: repeat(7, minmax(60px, auto));
  grid-template-columns: repeat(4, 60px);
  grid-gap: 12px;
  padding: 35px;
  font-family: "Poppins";
  font-weight: 300;
  font-size: 18px;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0px 3px 80px -30px rgba(13, 81, 134, 1);
}

.btn,
.zero {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #484848;
  background-color: #f4faff;
  border-radius: 5px;
}

.display,
.answer {
  grid-column: 1 / 5;
  display: flex;
  align-items: center;
}

.display {
  color: #a3a3a3;
  border-bottom: 1px solid #e1e1e1;
  margin-bottom: 15px;
  overflow: hidden;
  text-overflow: clip;
}

.answer {
  font-weight: 500;
  color: #146080;
  font-size: 55px;
  height: 65px;
}

.zero {
  grid-column: 1 / 3;
}

.operator {
  background-color: #d9efff;
  color: #3fa9fc;
}
</style>