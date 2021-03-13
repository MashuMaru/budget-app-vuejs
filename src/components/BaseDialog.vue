<template>
  <div>
    <dialog>
      <slot>
        <h2>You must enter a Salary first.</h2>
      </slot>
    </dialog>
  </div>
</template>

<script>
export default {};
</script>

<style>
div {
  color: white;
  background-color: red;
  width: 250px;
  height: 250px;
  text-align: center;
}

</style>
