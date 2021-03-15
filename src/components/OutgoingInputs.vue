<template>
  <div v-on:click="close">
    <Dialog v-if="!inputIsValid" />
    <h3>Outgoings</h3>
    <form v-on:submit.prevent="submitCosts">
      <input
        type="text"
        placeholder="Utility"
       
        ref="utilityInput"
        v-model="utility"
      />

      <input type="number" placeholder="Cost" ref="costInput" v-model="cost" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import Dialog from "./Dialog.vue";

export default {
  components: { Dialog },
  //NEW BELOW
  // inject: ["addCost"],
  //NEW ABOVE
  emits: ["cost-information"],
  data: function() {
    return {
      utility: "",
      cost: null,
      // cost: "",
      inputIsValid: true,
    };
  },
  methods: {
    submitCosts() {
      //NEW BELOW
      // const utilityName = this.$refs.utilityInput.value;
      // const utilityCost = this.$refs.costInput.value;
      //NEW ABOVE
      if (this.utility === "" && this.cost === null) {
        this.inputIsValid = false;
        // return;
      } else {
        this.$emit("cost-information", this.utility, this.cost);
        // this.addCost(utilityName, utilityCost);
        this.utility = "";
        this.cost = null;
      }
    },
    close() {
      this.inputIsValid = true;
    },
  },
};
</script>

<style></style>
