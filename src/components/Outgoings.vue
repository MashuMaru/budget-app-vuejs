<template>
  <div>
    <p>
      <span class="utility-nc">{{ utilityName }}: </span>
      <span class="utility-nc">£{{ utilityCost }}</span>
      <span><button class="utility-btn">X</button></span>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    utilityName: String,
    utilityCost: String,
  },
  data: function() {
    return {};
  },
};
</script>

<style scoped>
input {
  pointer-events: none;
  border-bottom: 1px solid green;
  text-align: center;
}

/* p {
  margin-bottom: 25px;
} */

.utility-nc {
  margin-left: 25px;
  margin-right: 25px;
  border-bottom: 1px solid #44A6A1;
  width: 150px;
  color: white;
}

.utility-btn {
  border: none !important;
}

.utility-btn:hover {
  background-color: transparent;
  color: #f39189;
}
</style>
