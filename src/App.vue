<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="screen">
      <input v-model.number="operand1" type="text" />
      {{ operator }}
      <input v-model.number="operand2" type="text" />
      <!-- Для примера у v-model есть такие модификаторы:
      ● .trim - автоматически обрезать пробелы в начале и в конце строки
      ● .lazy - v-model синхронизирует ввод с данными по событию input, чтобы использовать для
      синхронизации после события change
      ● .number - для автоматического приведения введённого пользователем к Number -->
      =>
      <input v-model="result" type="text" readonly />
    </div>



    <div v-if="error" class="error">{{error}}</div>
    <div class="keyboard">
      <div class="row">
        <!-- <button v-on:click="getResult('+')">+</button> -->
        <!-- v-on:click = @click -->
        <!-- <button v-for="item in operators" v-bind:key="item" @click="getResult (item)">{{ item }}</button> -->
        <!-- v-for нужна при переборе элементов для получения индекса элемента в массиве:-->
        <button v-for="(item, index) in operators" :key="index" @click="setOperator(item)">{{ item }}</button>
      </div>


      <input type="checkbox" id="checkbox" @click="checked = !checked" v-model="sqreenKeyboard" />
      <br>
      Отобразить экранную клавиатуру
      <br>
      <div v-if="sqreenKeyboard"></div>
      <button v-for="(item, index) in keys" :key="index" @click="setKeys(item)"> {{item}}</button>
    </div>
  </div>
  <ul>
    <li v-for="[time, msg] in Object.entries(log)" :key="time">{{time}}: {{msg}}</li>
  </ul>

</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      operand1: 0,
      operand2: 0,
      operator: '+',
      error: "",
      operators: ['+', '-', '*', '/', '**', '//'],
      keys: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '<---'],
      log: {}
    }
  },
  computed: {
    result() {
      this.error = '';
      //this.log[new Date().toTimeString()] = `${this.operand1} ${operator} ${this.operand2}` (в данном случае не будет обновлять строку при повторном нажатии)
      //this.$set(this.log, new Date().toTimeString(), `${this.operand1} ${operator} ${this.operand2}`)
      switch (this.operator) {
        case '+':
          return this.operand1 + this.operand2
          break;
        case '*':
          return this.operand1 * this.operand2
          break;
        case '-':
          return this.operand1 - this.operand2
          break;
        case '/':
          if (this.operand2 == 0) {
            this.error = 'На ноль делить нельзя'
          } else {
            return this.operand1 / this.operand2
          }
          break;
        case '**':
          return this.operand1 ** this.operand2
          break;
        case '//':
          return Math.floor(this.operand1 / this.operand2)
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
    // setKeys() {
    //   this.keys = this.keys
    // }
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
  margin: 30px;
  padding: 20 px;
  border: 1px solid red;
  background-color: blue;
  color: #cf1b4b
}
</style>


