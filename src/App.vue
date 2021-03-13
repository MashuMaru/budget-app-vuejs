<template>
  <div id="main">
    <Header />
    <Salary />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Salary from "./components/Salary.vue";

export default {
  components: { Header, Salary },
};
</script>

<style>
#main {
  width: 80%;
  height: 600px;
  margin-left: auto;
  margin-right: auto;
  background-color: black;
  border-radius: 25px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
</style>
