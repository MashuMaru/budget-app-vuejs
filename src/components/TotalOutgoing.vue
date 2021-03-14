<template>
  <div>
    <label for="outgoing">Total Outgoing: </label>
    <input
      id="outgoing"
      placeholder="outgoing"
      type="number"
      name="outgoing"
      v-model="outgoingCost"
      v-on:keyup="emitToApp"
    />
    <!-- <button>Add</button> -->
  </div>
</template>

<script scoped>
export default {
  emits: ["outgoingCost"],
  data: function() {
    return {
      outgoingCost: null,
    };
  },
  methods: {
    emitToApp(e) {
      this.outgoingCost = e.target.value;
      this.$emit("outgoingCost", this.outgoingCost);
    },
  },
};
</script>

<style scoped>
div {
  margin-top: 50px;
}
</style>
