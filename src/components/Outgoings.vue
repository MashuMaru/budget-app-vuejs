<template>
  <div>
    <div class="outgoings-section">
      <p>{{ utilityName }}:</p>
      <p>£{{ utilityCost }}</p>
      <button
        class="utility-btn"
        v-on:mouseover="mousedOver = true"
        v-on:mouseleave="mousedOver = false"
        name="delete"
        v-on:click="deleteUtility(id)">X</button>
    </div>
    <span> </span>
    <!-- <label for="delete" v-if="mousedOver">delete</label> -->
  </div>
</template>

<script>
export default {
  inject: ["deleteUtility"],
  props: {
    id: String,
    utilityName: String,
    utilityCost: Number,
  },
  data: function() {
    return {
      mousedOver: false,
    };
  },
};
</script>

<style scoped>
label {
  font-style: italic;
  font-size: 14px;
  position: absolute;
}

.utility-nc {
  margin-right: 10px;
  border-bottom: 1px solid #44a6a1;
  color: white;
}

.utility-btn {
  border: none !important;
  color: #f39189;
  transition: all 0.1s ease 0s;
}

.utility-btn:hover {
  background-color: transparent;
  color: #f39189;
  transition: transform 0.1s, visibility 0.1s ease-in;
  -ms-transform: scale(1.5);
  -webkit-transform: scale(1.5);
}

p {
  display: inline-block;
  margin-left: 15px;
  margin-top: 8px;
  margin-bottom: 8px;
}

.outgoings-section {
  margin-left: auto;
  margin-right: auto;
  display: inline-block;
  border-bottom: 1px solid #44a6a1;
  text-align: right;
  width: 250px;
}
</style>
