<template>
  <div>
    <div class="display">
      <input v-model.number="operand1" name="operand1" />
      <input v-model.number="operand2" name="operand2" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button
        v-for="op in operations"
        :key="op"
        @click="calculate(op)"
        :name="op"
      >
        {{ op }}
      </button>
    </div>
    <label>
      <input type="checkbox" v-model="showvk" />Отобразить клавиатуру</label
    >

    <div v-if="showvk">
      Виртуальная клавиатура
      <button v-for="btn in 10" :key="btn" @click="inputNum(btn - 1)">
        {{ btn - 1 }}
      </button>
      <button @click="eraseOne">E</button>
      <br />
      <label
        ><input type="radio" value="1" v-model="operch" name="operand" />Операнд
        1</label
      >
      <label
        ><input type="radio" value="2" v-model="operch" name="operand" />Операнд
        2</label
      >
    </div>
  </div>
</template>

<script>
  export default {
    name: "Calc",
    data() {
      return {
        operand1: "",
        operand2: "",
        result: "",
        operations: ["+", "-", "*", "/"],
        showvk: false,
        operch: "",
      };
    },
    methods: {
      calculate(op) {
        const operand1 = this.operand1;
        const operand2 = this.operand2;
        const calcOperations = {
          "+": () => operand1 + operand2,
          "-": () => operand1 - operand2,
          "/": () => operand1 / operand2,
          "*": () => operand1 * operand2,
        };
        this.result = calcOperations[op]();
      },
      inputNum(i) {
        const { operch } = this;
        const input = operch === "1" ? "operand1" : "operand2";
        this[input] = +(this[input] += String(i));
      },
      eraseOne() {
        const { operch } = this;
        const input = operch === "1" ? "operand1" : "operand2";
        this[input] = +String(this[input]).slice(0, -1);
      },
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
