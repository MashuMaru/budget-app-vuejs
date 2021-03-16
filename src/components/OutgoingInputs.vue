<template>
  <div v-on:click="close">
    <Dialog v-if="!inputIsValid" />
    <h3>Outgoings</h3>
    <form v-on:submit.prevent="submitCosts">
      <input
        type="text"
        placeholder="Name"
        maxlength="15"
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
  emits: ["cost-information"],
  data: function() {
    return {
      utility: "",
      cost: null,
      inputIsValid: true,
    };
  },
  methods: {
    submitCosts() {
      if (this.utility === "" || this.cost === null) {
        this.inputIsValid = false;
      } else {
        this.$emit("cost-information", this.utility, this.cost);
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

<style>
input[type=number] {
  -moz-appearance: textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
