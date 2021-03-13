<template>
  <div>
    <form action="submit">
      <label for="outgoing">Outgoing: </label>
      <input
        id="outgoing"
        placeholder="outgoing"
        type="number"
        name="outgoing"
        v-model="outgoingCost"
        v-on:keyup="emitToSalary"
      />
      <button>Add</button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["outgoingData"],
  data: function() {
    return {
      outgoingCost: null,
    };
  },
  methods: {
    emitToSalary(e) {
      this.outgoingCost = e.target.value;
      this.$emit("outgoingData", this.outgoingCost);
    },
  },
};
</script>

<style></style>
