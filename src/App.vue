<template>
  <div id="app">
    <header>
      <div class="title">My personal costs</div>
    </header>

    <main>
      <add-payment-form @addPayment="add" />
      <payments-display :items="paymentsList" />
    </main>
  </div>
</template>

<script>
  import AddPaymentForm from "./components/AddPaymentForm.vue";
  import PaymentsDisplay from "./components/PaymentsDisplay.vue";

  export default {
    name: "App",
    components: { PaymentsDisplay, AddPaymentForm },
    data() {
      return {
        show: false,
        paymentsList: [],
      };
    },
    methods: {
      add(data) {
        this.paymentsList = [...this.paymentsList, data];
      },
      fetchData() {
        return [
          {
            id: "1",
            date: "28.03.2020",
            category: "Food",
            value: 169,
          },
          {
            id: "2",
            date: "24.03.2020",
            category: "Transport",
            value: 360,
          },
          {
            id: "3",
            date: "24.03.2020",
            category: "Food",
            value: 532,
          },
        ];
      },
    },
    created() {
      this.paymentsList = this.fetchData();
    },
  };
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
</style>
