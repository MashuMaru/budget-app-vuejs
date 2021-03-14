<template>
  <div id="main">
    <Header title="Budget App" />
    <Salary v-on:outgoingSalary="salaryInput" v-on:keyup="calculate" />
    <Outgoing v-on:outgoingCost="outgoingSum" v-on:keyup="calculate" />
    <p v-if="(salaryIsNotFilled)">You have to enter a salary first.</p>
    <button v-on:click="calculate">Calculate</button>
    <p>Total: {{ total }}</p>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Salary from "./components/Salary.vue";
import Outgoing from "./components/Outgoing.vue";

export default {
  components: { Header, Salary, Outgoing },
  data: function() {
    return {
      salary: null,
      outgoing: null,
      total: null,
      salaryIsNotFilled: false,
    };
  },
  methods: {
    outgoingSum(value) {
      this.outgoing = parseInt(value);
    },
    salaryInput(value) {
      this.salary = parseInt(value);
    },
    calculate() {
      if (this.salary === null) {
        this.salaryIsNotFilled = true;
      } else {
        this.salaryIsNotFilled = false;
        this.total = this.salary - this.outgoing;
      }
    },
  },
};
</script>

<style>
#main {
  width: 80%;
  height: 600px;
  margin-left: auto;
  margin-right: auto;
  background-color: black;
  border-radius: 25px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
</style>
