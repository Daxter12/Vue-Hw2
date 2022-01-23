<template>
  <div>
    <div class="display">
      <input v-model.number="operand1" />
      <input v-model.number="operand2" />
      = {{ result }}
      <br />
      = {{ resultFib }}
    </div>

    <hr />

    <div class="keyboard">
      <button
        v-for="operand in operands"
        :key="operand"
        @click="calculate(operand)"
      >
        {{ operand }}
      </button>
    </div>

    <div v-if="error">Ошибка! {{ error }}</div>

    <div class="strange-message">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Получилось слишком большое число</template>
    </div>

    <hr />

    <div v-for="(item, index) in myCollection" :key="index">
      {{ index }} - {{ item }}
    </div>

    <div class="logs">
      <div v-for="(log, id) in logs" :key="id">{{ log }}</div>
    </div>
  </div>
</template>

<script>
  // import Vue from "vue";
  export default {
    name: "Calculator",
    data() {
      return {
        operand1: "",
        operand2: "",
        result: "",
        resultFib: 0,
        error: "",
        myCollection: [1, 2, 3, 4, 5, 6, 7, 8, 9],
        operands: ["+", "-", "*", "/"],
        logs: {},
      };
    },
    computed: {
      fib1() {
        return this.fib(this.operand1);
      },
      fib2() {
        return this.fib(this.operand2);
      },
    },
    methods: {
      calculate(operation = "+") {
        this.error = "";
        switch (operation) {
          case "+":
            this.add();
            break;
          case "-":
            this.substract();
            break;
          case "*":
            this.multiply();
            break;
          case "/":
            this.divide();
            break;
        }

        const key = Date.now();
        const value = `${this.operand1}${operation}${this.operand2}=${this.result}`;
        this.$set(this.logs, key, value);
      },

      add() {
        this.result = parseInt(this.operand1) + parseInt(this.operand2);
        this.resultFib = this.fib1 + this.fib2;
      },
      substract() {
        this.result = this.operand1 - this.operand2;
        this.resultFib = this.fib(this.operand1) - this.fib(this.operand2);
      },
      divide() {
        const { operand1, operand2 } = this;
        if (operand2 === 0) {
          this.error = "Делить на 0 нельзя!";
        } else {
          this.result = operand1 / operand2;
        }
      },
      multiply() {
        this.result = this.operand1 * this.operand2;
      },
      fib(n) {
        return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
      },
    },
    props: {
      msg: String,
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
