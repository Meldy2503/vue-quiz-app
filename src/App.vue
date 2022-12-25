<template>
  <div v-if="!startQuiz" class="wrapper">
    <div class="wrapper-contents">
      <div class="wrapper-img">
        <img src="./assets/icon6.png" alt="icon" />
      </div>
      <div class="wrapper-text">
        <h1>QUIZ APP</h1>
        <p>
          You are presented with questions and four options, you have 30 seconds
          to answer each question after which you will be automatically moved to
          the next question. Failure to select an answer within the time limit
          will result in a loss of points. At the end of the quiz, your total
          score will be displayed. Good luck!!
        </p>
        <button @click="AttemptQuiz()">Start Quiz</button>
      </div>
    </div>
  </div>
  <div v-show="startQuiz">
    <QuizQuestions />
  </div>
</template>

<script>
import QuizQuestions from "./components/QuizQuestions.vue";
export default {
  name: "App",
  data() {
    return {
      startQuiz: false,
    };
  },
  methods: {
    AttemptQuiz() {
      this.startQuiz = true;
    },
  },

  components: {
    QuizQuestions,
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

body. html {
  height: 100%;
  width: 100%;
}
body {
  font-family: "Poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
  position: relative;
}

.wrapper {
  background-image: url(./assets/pattern.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.wrapper-contents {
  margin: 0 auto;
  width: 90%;
  max-width: 1200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 20px;
  background-color: #f5f5f5;
  box-shadow: 10px 10px 42px 0px rgba(0, 0, 0, 0.3);
  padding: 100px 50px;
}

.wrapper-img {
  width: 45%;
}
.wrapper-img img {
  max-width: 100%;
  width: 100%;
  height: 350px;
  object-fit: cover;
  object-position: center;
}

.wrapper-text {
  width: 50%;
  text-align: center;
}

.wrapper-text h1 {
  font-size: 40px;
  font-weight: 900;
  margin-bottom: 10px;
}

.wrapper-text p {
  text-align: left;
  font-size: 17px;
  line-height: 1.8;
  margin-bottom: 20px;
}
.wrapper-text button {
  background-color: #4aaaac;
  border: none;
  outline: none;
  padding: 11px 30px;
  color: #fff;
  font-weight: 600;
  font-size: 17px;
  border-radius: 5px;
}

.wrapper-text button:hover {
  background-color: #6c757d;
}

/* media-queries */
@media (max-width: 960px) {
  .wrapper-contents {
    width: 95%;
  }
}
@media (max-width: 768px) {
  .wrapper {
    height: 100%;
  }
  .wrapper-contents {
    flex-direction: column;
    margin: 15px 0;
    padding: 30px 40px 60px 40px;
  }
  .wrapper-text {
    width: 100%;
  }
  .wrapper-img {
    width: 100%;
  }
  .wrapper-img img {
    height: 100%;
  }
}
@media (max-width: 500px) {
  .wrapper-contents {
    padding: 30px 20px 60px 20px;
  }
  .wrapper-text h1 {
    font-size: 30px;
  }
  .wrapper-text p {
    font-size: 16px;
  }
}
</style>
