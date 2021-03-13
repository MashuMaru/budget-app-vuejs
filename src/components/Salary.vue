<template>
  <div class="salary">
    <div>
      <label for="salary">Income: </label>
      <input
        placeholder="income"
        type="number"
        name="salary"
        id="salary"
        v-model="salary"
      />
    </div>
    <Outgoing v-on:outgoingData="outgoingSum" />

    <p>Total: {{ total }}</p>
  </div>
</template>

<script>
import Outgoing from "./Outgoing.vue";
export default {
  components: { Outgoing },
  data: function() {
    return {
      salary: null,
      outgoing: null,
      total: null,
    };
  },
  methods: {
    outgoingSum(value) {
      this.outgoing = value;
      this.total = parseInt(this.salary) + parseInt(this.outgoing)
    },
  },
};
</script>

<style scoped>
label {
  color: white;
}

p {
  color: white;
}
</style>
