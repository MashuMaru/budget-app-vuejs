<template>
  <div>
    <div>
      <span class="utility-nc">{{ utilityName }}: </span>
      <span class="utility-nc">£{{ utilityCost }}</span>
      <span>
        <button
          class="utility-btn"
          v-on:mouseover="mousedOver = true"
          v-on:mouseleave="mousedOver = false"
          name="delete">
          X
        </button>
        </span>
      <label for="delete" v-if="mousedOver">delete</label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    utilityName: String,
    utilityCost: String,
  },
  data: function() {
    return {
      mousedOver: false,
    };
  },
};
</script>

<style scoped>
input {
  pointer-events: none;
  border-bottom: 1px solid green;
  text-align: center;
}

label {
  font-style: italic;
  font-size: 14px;
  position: absolute;
}

.utility-nc {
  margin-left: 25px;
  margin-right: 25px;
  border-bottom: 1px solid #44a6a1;
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
