<template>
  <div v-on:click="close">
    <Dialog v-if="!inputIsValid" />
    <h3>Outgoings</h3>
    <form v-on:submit.prevent="submitCosts">
      <input type="text" placeholder="Utility" v-model="utility" />
      <input type="text" placeholder="Cost" v-model="cost" />
      <button>Add</button>
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
      cost: "",
      inputIsValid: true,
    };
  },
  methods: {
    submitCosts() {
      if (this.utility === "" && this.cost === "") {
        this.inputIsValid = false;
      } else {
        this.$emit("cost-information", this.utility, this.cost);
        this.utility = "";
        this.cost = "";
      }
    },
    close() {
      this.inputIsValid = true;
    },
  },
};
</script>

<style></style>
