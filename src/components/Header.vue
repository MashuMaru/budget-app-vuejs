<template>
  <div id="header">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
    },
  },
};
</script>

<style>
#header {
  width: 100%;
  height: 75px;
  color: white;
  padding: auto;
  margin-bottom: 25px;
}

h1 {
  padding-top: 25px;
  /* margin-bottom: 15px; */
  font-size: 25px;
}

</style>
