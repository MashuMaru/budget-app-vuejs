<template>
  <div>
    <p>
      <span class="utility-nc">{{ utilityName }}: </span>
      <span class="utility-nc">{{ utilityCost }}</span>
      <span><button class="utility-btn">X</button></span>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    utilityName: {
      type: String,
    },
    utilityCost: {
      type: Number,
    },
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

p {
  margin-bottom: 25px;
}

.utility-nc {
  margin-left: 25px;
  margin-right: 25px;
  border-bottom: 1px solid green;
  width: 150px;
  color: white;
}

.utility-btn {
  border: none !important; 

}

.utility-btn:hover {
  border-radius:100% !important; 
  background-color: red;
}
</style>
