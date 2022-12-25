<template>
  <div class="overlay">
    <div class="alert">
      <p>Thanks for playing&#x1F60D;</p>
      <h2>Your score is <br />{{ totalPoints }}/{{ totalQuestions }}</h2>
      <a href="/">Play Again</a>
    </div>
  </div>
</template>
<script>
export default {
  name: "TotalPoints",
  props: ["totalPoints", "totalQuestions"],
};
</script>
<style scoped>
.overlay {
  background-color: rgb(0, 0, 0, 0.9);
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.alert {
  width: 300px;
  background-color: #fff;
  color: #090909;
  padding: 50px 20px;
  border-radius: 15px;
  text-align: center;
}

p {
  font-size: 21px;
  font-weight: 600;
}
h2 {
  padding: 20px 0 35px 0;
  font-size: 28px;
  font-weight: 800;
}

a {
  padding: 12px 35px;
  text-align: center;
  background-color: #4aaaac;
  color: #fff;
  border: none;
  text-decoration: none;
  border-radius: 5px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.7s ease 0s;
}

a:hover {
  background-color: #6c757d;
}

/* media queries */
@media (max-width: 350px) {
  .alert {
    width: 260px;
    padding: 42px 10px;
  }
}
</style>
