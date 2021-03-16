<template>
  <div class="total-section">
    <label for="outgoing">Total Outgoing: </label>
    <p>{{ total }}</p>
    <!-- <input
      id="outgoing"
      placeholder="outgoing"
      type="number"
      name="outgoing"
      v-model="outgoingCost"
      v-on:keyup="emitToApp"
    /> -->
  </div>
</template>

<script scoped>
export default {
  emits: ["outgoingCost"],
  props: ['total'],
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
/* div {
  margin-top: 50px;
} */

.total-section {
  margin-bottom: 25px;
  margin-top: 25px;
}

p {
  display: inline-block;
  /* margin-right: 15px; */
  margin-left: 15px;
  border-bottom: 1px solid #44a6a1;
  /* border-bottom: 1px solid #44a6a1;  */
}

.total-section {
  margin-left: auto;
  margin-right: auto;
  /* display: inline-block; */
  text-align: center;
  width: 250px;
}
</style>
