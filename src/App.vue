<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="screen">
      <input v-model.number="operand1" type="text" />
      {{ operator }}
      <input v-model.number="operand2" type="text" />
      =>
      <input v-model="result" type="text" readonly />
    </div>
    <div v-if="error" class="error"> {{error}}</div>

    <div class="keyboard">
      <div class="row">
        <button v-for="(item, index) in operators" v-bind:key="index" @click="setOperator(item)">{{ item }}</button>
      </div>
    </div>
    <Second v-bind:username='author'> </Second>
    <ul>
      <li v-for="[time,msg] in Object.entries(log)" :key="time">{{time}}: {{msg}} </li>
    </ul>



    <input type="checkbox" id="checkbox" @click="checked = !checked" v-model="checked">
    <label for=" checkbox"> Отобразить экранную клавиатуру</label>

    <div class="sqreenKeyboard" v-if="checked">
      <button v-for="(item, index) in numbers" :key="index" @click="getNumber(item)">
        {{item}}</button>

      <!-- <keyboard @addNum="addNumber" @delNum="delNumber" /> -->
    </div>


  </div>
</template>

<script>
import Second from './components/Second.vue'

export default {
  name: "App",
  comments: {
    Second
  },
  data() {
    return {
      operator: '+',
      operand1: 0,
      operand2: 0,
      error: "",
      operators: ["+", "-", "*", "/", "**", "//"],
      checked: [],
      numbers: [0, 1, 2, 3, 5, 6, 7, 8, 9],
      author: 'Admin',
      log: {},
      checked: false

    };
  },
  computed: {
    result() {
      this.error = "";
      //this.log[new Date().toTimeString()] = `${this.operand1} ${operator} ${this.operand2}`
      //  this.$set(this.log, new Date().toTimeString(), `${this.operand1} ${operator} ${this.operand2}`)

      switch (this.operator) {
        case "+":
          return this.operand1 + this.operand2;
          break;
        case "-":
          return this.operand1 - this.operand2;
          break;
        case "*":
          return this.operand1 * this.operand2;
          break;
        case "/":
          if (this.operand2 == 0) {
            this.error = "На ноль делить нельзя";
          }
          else {
            return this.operand1 / this.operand2;
            break;
          }
        case "**":
          return this.operand1 ** this.operand2;
          break;
        case "//":
          return Math.floor(this.operand1 / this.operand2);
          break;
        default:
          return 0
          break;

      }

    }
  },


  methods: {
    setOperator(operator) {
      this.operator = operator
    },
    getResult(operator) {

    },
    getNumber(numbers) {
      this.operand1 = numbers;
      this.operand2 = numbers;
    },
    components: { Second }

  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.error {
  margin: 20px;
  padding: 20px;
  border: 1px solid rgb(112, 55, 55);
  background-color: rgb(231, 89, 89);
  color: rgb(112, 55, 55);
}
</style>
