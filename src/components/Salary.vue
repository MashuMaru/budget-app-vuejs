<template>
  <div class="salary">
    <form action="submit">
      <label for="salary">Income: </label>
      <input
        placeholder="income"
        type="number"
        name="salary"
        id="salary"
        v-on:keyup="emitToApp"
        v-model="salary"
      />
    </form>
  </div>
</template>

<script>
export default {
  emits: ["outgoingSalary"],
  data: function() {
    return {
      salary: null,
    };
  },
  methods: {
    emitToApp(e) {
      this.salary = e.target.value;
      this.$emit("outgoingSalary", this.salary);
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
