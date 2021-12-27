<template>
  <div>
    <h1> CALCULATOR</h1>
    <div class="calculator">
      <div class="display">{{ current || "0" }}</div>
      <div @click="clear" class="button">AC</div>
      <div @click="two" class="button">+/-</div>
      <div @click="percent" class="button">%</div>
      <div @click="divide" class="operator">/</div>
      <div @click="append('7')" class="button">7</div>
      <div @click="append('8')" class="button">8</div>
      <div @click="append('9')" class="button">9</div>
      <div @click="multiply" class="operator">*</div>
      <div @click="append('4')" class="button">4</div>
      <div @click="append('5')" class="button">5</div>
      <div @click="append('6')" class="button">6</div>
      <div @click="minus" class="operator">-</div>
      <div @click="append('1')" class="button">1</div>
      <div @click="append('2')" class="button">2</div>
      <div @click="append('3')" class="button">3</div>
      <div @click="add" class="operator">+</div>
      <div @click="append(0)" class="button">0</div>
      <div @click="del" class="button">DEL</div>

      <div @click="dot" class="button">.</div>
      <div @click="equal" class="operator">=</div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Calculator",
  setup() {
    let current = ref("");
    let previous = ref(null);
    let operator = ref(null);
    let operatorClick = ref(false);
    function clear() {
      current.value = "";
    }
    function two() {
      current.value =
        current.value.charAt(0) === "-"
          ? current.value.slice(1)
          : `-${current.value}`;
    }
    function percent() {
      current.value = `${current.value / 100}`;
    }
    function append(number) {
      if (operatorClick.value) {
        current.value = "";
        operatorClick.value = false;
      }
      current.value = `${current.value}${number}`;
    }
    function dot() {
      if (current.value.indexOf(".") === -1) {
        `${append(".")}`;
      }
    }
    function del() {
      current.value = current.value.slice(0, -1);
    }
    function setPrevious() {
      previous.value = current.value;
      operatorClick.value = true;
    }
    function divide() {
      operator.value = (a, b) => a / b;
      setPrevious();
    }
    function multiply() {
      operator.value = (a, b) => a * b;
      setPrevious();
    }
    function minus() {
      operator.value = (a, b) => a - b;
      setPrevious();
    }
    function add() {
      operator.value = (a, b) => a + b;
      setPrevious();
    }
    function equal() {
      current.value = operator.value(
        parseFloat(previous.value),
       parseFloat(current.value)
      );
      console.log(current.value);
      console.log(previous.value);
      previous.value=null;
    }
    return {
      current,  
      previous,
      operator,
      operatorClick,
      clear,
      two,
      percent,
      append,
      dot,
      del,
      setPrevious,
      divide,
      multiply,
      minus,
      add,
      equal,
    };
  },
};
</script>

<style>
* {
  background: black;
}
#app {
  margin-top: 0px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 15px;
}
.calculator {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  display: grid;
  grid-auto-rows: minmax(50px, auto);
  grid-template-columns: repeat(4, 1fr);
  font-size: 25px;
  width: 300px;
  margin: 0 auto;
  margin-bottom: 0px;
  text-align: center;
  background: rgb(46, 46, 46);
  padding: 10px 5px;
  border-radius: 30px;
  box-shadow: 0px 0px 20px 0px rgba(255, 238, 0, 0.246);
}
.button {
  background: rgb(77, 77, 77);
  color: #7fff00;
  border-radius: 50px;
  margin: 5px;
  padding: 20px 5px 20px 5px;
  margin-top: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.4);
}
.button:hover {
  background: rgb(58, 58, 58);
  color: rgb(84, 168, 0);
}
.button:active {
  background: rgb(82, 82, 82);
  color: rgb(84, 168, 0);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.1), 0 6px 20px 0 rgba(0, 0, 0, 0.1);
}
.display {
  grid-column: 1/5;
  background: rgb(82, 82, 82);
  color: tomato;
  text-align: right;
  border-radius: 30px;
  padding: 20px 0px;
  width: 300px;
  text-overflow: ellipsis;
  overflow: hidden;
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.4), inset;
}
.operator {
  background: chartreuse;
  color: #2c3e50;
  border-radius: 50px;
  margin: 5px;
  padding: 20px 5px 20px 5px;
  margin-top: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4), 0 6px 20px 0 rgba(0, 0, 0, 0.4);
}
.operator:hover {
  background: rgb(92, 184, 0);
}
.operator:active {
  background: rgb(62, 124, 0);
}
</style>