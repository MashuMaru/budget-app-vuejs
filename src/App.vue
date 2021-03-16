<template>
  <div class="main-background">
    <div id="main">
      <Header title="Budget App" />
      <Salary
        v-on:outgoingSalary="salaryInput"
        v-on:click="salaryIsNotFilled = false"
        v-on:keyup="calculate"
      />
      <OutgoingInputs v-on:cost-information="addExpenditure" />
      <div class="outgoings-scroll">
        <Outgoings
          v-for="cost in costInformation"
          v-bind:key="cost.id"
          v-bind:id="cost.id"
          v-bind:utilityName="cost.utility"
          v-bind:utilityCost="cost.cost"
        />
      </div>
      <TotalOutgoing v-bind:total="outgoing" />
      <p class="error-text" v-if="salaryIsNotFilled">
        You have to enter an income first.
      </p>
      <button v-on:click="calculate">Calculate</button>
      <p class="total">
        Remaining balance:
        <span class="total-span" v-bind:class="{ belowZero: numBelowZero }">£{{ total }}</span>
        <span v-if="numBelowZero" class="belowZero"><p>Whooa... Gone a bit below there.</p></span>
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
  emits: ["total-outgoing"],
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
        // {
        //   id: "first-entry",
        //   utility: "One",
        //   cost: 1000,
        // },
      ],
      numBelowZero: false,
    };
  },
  methods: {
    outgoingSum(value) {
      this.outgoing = value;
    },
    salaryInput(value) {
      this.salary = parseInt(value);
    },
    calculate() {
      const objectTotal = this.costInformation.map((cost) => cost.cost);
      const totalSum = objectTotal.reduce((acc, item) => acc + item, 0);
      console.log("total outgoing: " + totalSum);
      this.outgoing = "£" + totalSum;

      if (this.salary === null) {
        this.salaryIsNotFilled = true;
        //REMOVED THE BELOW INCASE CHANGE OCCURS ON INCOME
        // this.outgoing = null;
        //REMOVED THE ABOVE INCASE CHANGE OCCURS ON INCOME
      } else {
        this.salaryIsNotFilled = false;
        const remain = (this.total = this.salary - totalSum);
        if (remain <= 0) {
          this.numBelowZero = true;
          console.log("numZero is set to:" + this.numBelowZero + remain);
        } else {
          this.numBelowZero = false;
        }
        if (this.numBelowZero === true) {
          return "belowZero";
        } else {
          return null;
        }
      }
    },
    addExpenditure(utilityName, utilityCost) {
      if (utilityName === "" && utilityCost === "") {
        this.outgoingIsNotFilled = true;
      } else {
        const newCost = {
          id: new Date().toISOString(),
          utility: utilityName,
          cost: parseInt(utilityCost),
        };
        console.log(newCost);
        this.costInformation.unshift(newCost);
      }
      this.calculate();
    },
    deleteUtility(costId) {
      const thisUtility = this.costInformation
        .map((cost) => cost.id)
        .indexOf(costId);
      this.costInformation.splice(thisUtility, 1);
      this.outgoing = null;
      this.calculate();
    },
  },
};
</script>

<style>
html {
  height: 100vh;
  padding: 0;
  background-color: #14121b;
  overflow: hidden;
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
  max-height: 900px;
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
  overflow: hidden;
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
  transition: all 0.5s ease 0s;
}

button:hover {
  border: 1px solid #2fac97;
  background-color: #2fac97;
  color: black;
  transition: transform 0.5s, visibility 0.5s ease-in;
  -ms-transform: scale(1.05);
  -webkit-transform: scale(1.05);
}

.total {
  color: white;
  margin-top: 25px;
  margin-bottom: 50px;
}

.total-span {
  color: #44a6a1;
  font-weight: bold;
}

.error-text {
  margin-bottom: 15px;
  font-weight: bold;
  font-style: italic;
  color: #f74e3f;
}

.outgoings-scroll {
  overflow: auto;
  max-height: 400px;
}

@media only screen and (max-height: 1000px) {
  .outgoings-scroll {
    max-height: 200px;
  }
}

.belowZero {
  color: #f39189 !important;
}
</style>
