<template teleport to="body">
  <div v-on:click="$emit('close')"></div>
  <dialog open>
      <h1>Invalid outgoing inputs.</h1>
      <p>Please add a utility and a cost to add to the list.</p>
      <button v-on:click="$emit('close')">Got it!</button>
  </dialog>
</template>

<script>
export default {

}
</script>

<style scoped>
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

dialog {
  position: fixed;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0;
  margin: 0;
  overflow: hidden;
}

button {
    background-color: black;
    margin-bottom: 15px;
    margin-top: 15px;
}

</style>