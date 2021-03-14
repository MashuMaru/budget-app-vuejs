<template>
  <div id="main">
    <Header title="Budget App" />
    <Salary v-on:outgoingSalary="salaryInput" />
    <!-- v-on:keyup="calculate" add back to <Salary /> for calculation on entering keys -->
    <OutgoingInputs v-on:cost-information="addExpenditure" />
    <Outgoings
      v-for="cost in costInformation"
      v-bind:key="cost"
      v-bind:id="cost.id"
      v-bind:utilityName="cost.utility"
      v-bind:utilityCost="cost.cost"
    />
    <TotalOutgoing v-on:outgoingCost="outgoingSum" />
    <!-- v-on:keyup="calculate" add back to <TotalOutgoing /> for calculation on entering keys -->
    <p v-if="salaryIsNotFilled">You have to enter a salary first.</p>
    <button v-on:click="calculate">Calculate</button>
    <p class="total">
      Remaining budget: <span class="total-span"> {{ total }} </span>
    </p>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Salary from "./components/Salary.vue";
import TotalOutgoing from "./components/TotalOutgoing.vue";
import OutgoingInputs from "./components/OutgoingInputs.vue";
import Outgoings from "./components/Outgoings.vue";

export default {
  // provide: function() {
  //   return {
  //     costInfo: this.costInformation,
  //   };
  // },
  components: { Header, Salary, TotalOutgoing, OutgoingInputs, Outgoings },
  data: function() {
    return {
      salary: null,
      outgoing: null,
      total: null,
      salaryIsNotFilled: false,
      costInformation: [
        {
          id: "first-entry",
          utility: "Rent",
          cost: "1000",
        },
      ],
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
        this.total = "£" + (this.salary - this.outgoing);
      }
    },
    addExpenditure(utilityName, utilityCost ) {
      const newCost = {
        id: new Date().toISOString(),
        utility: utilityName,
        cost: utilityCost,
      }
      this.costInformation.unshift(newCost);
    }
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
input {
  width: 150px;
  border: none;
  border-bottom: 1px solid white;
  background-color: transparent;
  color: white;
  outline: none;
  padding-bottom: 10px;
  padding-left: 10px;
  margin-left: 10px;
  margin-right: 20px;
  margin-bottom: 20px;
}

button {
  border: 1px solid white;
  background-color: transparent;
  color: white;
  border-radius: 10px;
  padding: 10px;
  cursor: pointer;
  outline: none;
}

button:hover {
  border: 1px solid white;
  background-color: white;
  color: black;
}

.total {
  color: white;
}

.total-span {
  color: green;
  font-weight: bold;
}
</style>
