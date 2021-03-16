<template>
  <div class="total-section">
    <label for="outgoing">Total Outgoing: </label>
    <p>{{ total }}</p>
  </div>
</template>

<script scoped>
export default {
  emits: ["outgoingCost"],
  props: ["total"],
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
.total-section {
  margin-bottom: 25px;
  margin-top: 25px;
}

p {
  display: inline-block;
  margin-left: 15px;
  border-bottom: 1px solid #44a6a1;
  width: 50px;
}

.total-section {
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  width: 250px;
}
</style>
