<template>
  <div class="main-background">
    <div id="main">
      <Header title="Budget App" />
      <Salary
        v-on:outgoingSalary="salaryInput"
        v-on:click="salaryIsNotFilled = false"
      />
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
      <p class="error-text" v-if="salaryIsNotFilled">
        You have to enter a salary first.
      </p>
      <button v-on:click="calculate">Calculate</button>
      <p class="total">
        Remaining budget: <span class="total-span"> {{ total }} </span>
      </p>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Salary from "./components/Salary.vue";
import TotalOutgoing from "./components/TotalOutgoing.vue";
import OutgoingInputs from "./components/OutgoingInputs.vue";
import Outgoings from "./components/Outgoings.vue";

export default {
  provide: function() {
    return {
      deleteUtility: this.deleteUtility,
    };
  },
  components: {
    Header,
    Salary,
    TotalOutgoing,
    OutgoingInputs,
    Outgoings,
  },
  data: function() {
    return {
      salary: null,
      outgoing: null,
      total: null,
      salaryIsNotFilled: false,
      outgoingIsNotFilled: false,
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
    addExpenditure(utilityName, utilityCost) {
      if (utilityName === "" && utilityCost === "") {
        this.outgoingIsNotFilled = true;
        // alert("INVALID INPUTS.");
      } else {
        const newCost = {
          id: new Date().toISOString(),
          utility: utilityName,
          cost: utilityCost,
        };
        this.costInformation.unshift(newCost);
      }
    },
    deleteUtility(utilityId) {
      const thisUtility = this.costInformation.filter(cost => cost.id === utilityId);
      this.costInformation.splice(thisUtility, 1);
    }
  },
};
</script>

<style>
html {
  padding: 0;
  background-color: #14121b;
}

* {
  margin: 0;
  padding: 0;
}

.main-background {
  background-color: #14121b;
  height: 100vh;
  margin: 0;
  padding: 0;
}
#main {
  width: 80%;
  max-width: 500px;
  min-height: 600px;
  margin-left: auto;
  margin-right: auto;

  background-color: #2a253a;
  border-radius: 25px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
input {
  width: 100px;
  border: none;
  border-bottom: 1px solid #44a6a1;
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
  border: 1px solid #328dad;
  background-color: transparent;
  color: white;
  border-radius: 10px;
  padding: 10px;
  cursor: pointer;
  /* outline: none; */
}

button:hover {
  border: 1px solid #2fac97;
  background-color: #2fac97;
  color: black;
}

.total {
  color: white;
  margin-top: 25px;
}

.total-span {
  color: #44a6a1;
  font-weight: bold;
}

.error-text {
  margin-bottom: 15px;
  font-weight: bold;
  font-style: italic;
}
</style>
