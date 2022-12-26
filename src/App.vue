<template>
  <QuizApp />
</template>

<script>
import QuizApp from "./components/QuizQuestions.vue";
export default {
  name: "App",

  components: {
    QuizApp,
  },
};
</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body,
html {
  height: 100%;
  width: 100%;
  position: relative;
}
body {
  font-family: "Poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
}
</style>
