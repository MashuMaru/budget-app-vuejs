<template>
  <div>
    <h3>Outgoings</h3>
    <form v-on:submit.prevent="submitCosts">
      <input type="text" placeholder="Utility" v-model="utility" />
      <input type="text" placeholder="Cost" v-model="cost" />
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["cost-information"],
  data: function() {
    return {
      utility: "",
      cost: "",
    };
  },
  methods: {
    submitCosts() {
      this.$emit("cost-information", {
        utility: this.utility,
        cost: this.cost,                         
      });
    },
  },
};
</script>

<style></style>
