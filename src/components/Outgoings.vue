<template>
  <div>
    <input type="text" name="" id="utility"/>
    <input type="text" name="" id="cost" v-on:cost-information="cost" />
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      costInformation: [
        {
          id: "first-entry",
          utility: "Rent",
          cost: "£1000",
        },
      ],
    };
  },
  methods: {
    addCostUtility(name, cost) {
      const newCost = {
        id: new Date().toISOString(),
        utility: name,
        cost: cost,
      };
      this.costInformation.push(newCost);
    },
  },
};
</script>

<style scoped>
input {
  pointer-events: none;
  border-bottom: 1px solid green;
  text-align: center;
}
</style>
