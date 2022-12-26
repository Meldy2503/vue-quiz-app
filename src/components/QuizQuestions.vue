<template>
  <!-- welcome page -->
  <div v-show="!startQuiz" class="landingPage">
    <div class="landingPage-contents">
      <div class="landingPage-img">
        <img src="../assets/icon6.png" alt="icon" />
      </div>
      <div class="landingPage-text">
        <h1>QUIZ APP</h1>
        <p>
          You are presented with questions and four options, you have 30 seconds
          to answer each question after which you will be automatically moved to
          the next question. Failure to select an answer within the time limit
          will result in a loss of points. At the end of the quiz, your total
          score will be displayed. Good luck!!
        </p>
        <button @click="handleStartQuiz()">Start Quiz</button>
      </div>
    </div>
  </div>

  <!-- start quiz page -->
  <div class="question_container" v-show="startQuiz">
    <div class="question-contents">
      <p class="question-no">
        Question {{ currentQuestion }} of {{ questions.length }}
      </p>
      <h3 :class="countDown < 10 ? 'warning' : 'count-down'">
        {{ countDown }}
      </h3>
      <p class="question">
        {{ questions[currentQuestion - 1].question }}
      </p>
      <div class="options-container">
        <button
          type="button"
          v-for="(item, index) in questions[currentQuestion - 1].options"
          :key="index"
          @click="correctAnswer(item.isCorrect)"
        >
          {{ item.answer }}
        </button>
      </div>
      <div class="btn">
        <button
          class="next-btn"
          v-show="currentQuestion < questions.length"
          @click="handleNextQuestion()"
        >
          Next
        </button>
        <button
          class="submit-btn"
          v-show="currentQuestion === questions.length"
          @click="displayResult()"
        >
          Submit
        </button>
      </div>
    </div>
  </div>

  <!-- display result -->
  <TotalPoints
    v-show="showResult"
    :totalPoints="points"
    :totalQuestions="questions.length"
  />
</template>

<script>
import TotalPoints from "./TotalPoints.vue";
export default {
  name: "QuizApp",
  props: ["totalPoints", "totalQuestions", "countDownTimerFn"],
  data() {
    return {
      currentQuestion: 1,
      points: 0,
      countDown: 30,
      timer: null,
      startQuiz: false,
      showResult: false,
      questions: [
        {
          id: 1,
          question: "Which Vue directive is used for two-way binding?",
          options: [
            { answer: "v-on", isCorrect: false },
            { answer: "v-else", isCorrect: false },
            { answer: "v-model", isCorrect: true },
            { answer: "v-if", isCorrect: false },
          ],
        },
        {
          id: 2,
          question: "Who is the creator of vueJS ?",
          options: [
            { answer: "Jeff Bezos", isCorrect: false },
            { answer: "Elon Musk", isCorrect: false },
            { answer: "Evan You", isCorrect: true },
            { answer: "Tony Stark", isCorrect: false },
          ],
        },
        {
          id: 3,
          question: "All are examples of vue directives EXCEPT",
          options: [
            { answer: "v-model", isCorrect: false },
            { answer: "v-cloak", isCorrect: false },
            { answer: "v-on", isCorrect: false },
            { answer: "v-off", isCorrect: true },
          ],
        },

        {
          id: 4,
          question: "Which version of Vue was Launched on 2020?",
          options: [
            { answer: "Vue 2", isCorrect: false },
            { answer: "Vue 1", isCorrect: false },
            { answer: "Vue 4", isCorrect: false },
            { answer: "Vue 3", isCorrect: true },
          ],
        },
        {
          id: 5,
          question: "All are examples of life cyle methods in EXCEPT",
          options: [
            { answer: "isMounted()", isCorrect: true },
            { answer: "beforeMount()", isCorrect: false },
            { answer: "created()", isCorrect: false },
            { answer: "updated()", isCorrect: false },
          ],
        },
        {
          id: 6,
          question: "Which of the following is NOT a Javascript Framework",
          options: [
            { answer: "Vue", isCorrect: false },
            { answer: "Styled-Components", isCorrect: true },
            { answer: "React", isCorrect: false },
            { answer: "Angular", isCorrect: false },
          ],
        },
        {
          id: 7,
          question: "Composition API can be used on which version?",
          options: [
            { answer: "Vue 5", isCorrect: false },
            { answer: "Vue 2 Only", isCorrect: false },
            { answer: "Vue 3 Only", isCorrect: false },
            { answer: "Both Vue 2 and Vue 3", isCorrect: true },
          ],
        },
        {
          id: 8,
          question: "What is the full form of NPM?",
          options: [
            {
              answer: "New Package Manager",
              isCorrect: false,
            },
            {
              answer: "Node Packet Manager",
              isCorrect: false,
            },
            {
              answer: "Node Package Manage",
              isCorrect: false,
            },
            {
              answer: "Node Package Manager",
              isCorrect: true,
            },
          ],
        },
        {
          id: 9,
          question:
            "Which of the following directives is used for iteration in Vuejs",
          options: [
            { answer: "v-model", isCorrect: false },
            { answer: "v-for", isCorrect: true },
            { answer: "v-if", isCorrect: false },
            { answer: "v-show", isCorrect: false },
          ],
        },
        {
          id: 10,
          question: "Did you enjoy using this app?",
          options: [
            { answer: "yes", isCorrect: true },
            { answer: "no", isCorrect: false },
            { answer: "not sure", isCorrect: false },
            {
              answer: "don't want to answer",
              isCorrect: false,
            },
          ],
        },
      ],
    };
  },

  methods: {
    handleStartQuiz() {
      this.startQuiz = true;
      this.countDownTimer();
    },

    correctAnswer(isCorrect) {
      if (isCorrect) {
        this.points += 1;
      } else {
        this.points;
      }
    },

    displayResult() {
      this.showResult = true;
      this.countDown = 1;
    },

    countDownTimer() {
      if (this.countDown > 0) {
        this.timer = setTimeout(() => {
          this.countDown--;
          this.countDownTimer();
        }, 1000);
      } else if (this.countDown === 0) {
        if (this.currentQuestion === this.questions.length) {
          this.displayResult();
        } else {
          this.handleNextQuestion();
        }
      }
    },

    handleNextQuestion() {
      clearTimeout(this.timer);
      this.currentQuestion += 1;
      this.countDown = 30;
      this.countDownTimer();
    },
  },

  components: {
    TotalPoints,
  },
};
</script>

<style scoped>
.wrapper {
}
/* landing page stles */
.landingPage {
  background-image: url(../assets/pattern.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.landingPage-contents {
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

.landingPage-img {
  width: 47%;
}
.landingPage-img img {
  max-width: 100%;
  width: 100%;
  height: 350px;
  object-fit: cover;
  object-position: center;
}

.landingPage-text {
  width: 48%;
  text-align: center;
}

.landingPage-text h1 {
  font-size: 40px;
  font-weight: 900;
  margin-bottom: 10px;
}

.landingPage-text p {
  text-align: left;
  font-size: 17px;
  line-height: 1.8;
  margin-bottom: 20px;
}
.landingPage-text button {
  background-color: #4aaaac;
  border: none;
  outline: none;
  padding: 12px;
  width: 150px;
  color: #fff;
  font-weight: 600;
  font-size: 17px;
  border-radius: 5px;
  cursor: pointer;
  text-align: center;
  transition: all 0.7s ease 0s;
}

.landingPage-text button:hover {
  background-color: #6c757d;
}

/* quiz question section styles  */
.question-container {
  margin: 0 auto;
  max-width: 1200px;
  text-align: center;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
}
.question-contents {
  background-image: linear-gradient(
      to left top,
      rgb(255, 255, 255, 0.7),
      rgb(252, 252, 252, 0.7)
    ),
    url(../assets/pattern.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  padding: 30px 0 40px 0;
  width: 60%;
  margin: 70px auto;
  border-radius: 15px;
  color: #090909;
  box-shadow: 10px 10px 42px 0px rgba(0, 0, 0, 0.2);
  text-align: center;
}

.question-no {
  font-size: 25px;
  font-weight: 600;
  margin-bottom: 30px;
}

.question {
  font-size: 18px;
  font-weight: 600;
  text-align: center;
  line-height: 1.4;
  margin-bottom: 15px;
  padding: 0 20px;
}

.options-container {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: flex-start;
}

.options-container button {
  box-shadow: 0.03rem 0.06rem 0.1rem #090909;
  cursor: pointer;
  background-color: #4aaaac;
  color: #fff;
  font-size: 18px;
  width: 70%;
  font-weight: 600;
  padding: 13px;
  margin: 13px auto 0 auto;
  border-radius: 5px;
  border: none;
  text-align: center;
  outline: none;
}

.options-container button:hover {
  background-color: #f03559;
}
.options-container button:focus {
  background-color: #ecae10;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70%;
  margin: 0 auto;
}

.btn .next-btn,
.btn .submit-btn {
  width: 150px;
  padding: 9px;
  margin-top: 13px;
  border-radius: 5px;
  border: 2.9px solid #333;
  background-color: transparent;
  color: #000;
  font-size: 17px;
  font-weight: 600;
  cursor: pointer;
  text-align: center;
  outline: none;
  margin-top: 40px;
  outline: none;
  transition: all 0.7s ease 0s;
}

.btn .next-btn:hover,
.btn .submit-btn:hover {
  color: #fff;
  background-color: #333;
}

.count-down {
  font-size: 32px;
  font-weight: 600;
  border: 3px solid #333;
  border-radius: 50%;
  width: 82px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px auto;
}

.warning {
  font-size: 32px;
  font-weight: 600;
  border: 3px solid #f00909;
  color: #f00909;
  border-radius: 50%;
  width: 82px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px auto;
}

/* media-queries */
@media (max-width: 1280px) {
  .question-contents {
    width: 70%;
  }
}
@media (max-width: 960px) {
  .landingPage-contents {
    width: 95%;
    padding: 100px 40px;
  }

  .question-contents {
    width: 80%;
  }
  .options-container button {
    width: 80%;
  }
}

@media (max-width: 767px) {
  .landingPage {
    height: 100%;
  }
  .landingPage-contents {
    flex-direction: column;
    margin: 15px 0;
    padding: 30px 40px 60px 40px;
  }
  .landingPage-text {
    width: 100%;
  }
  .landingPage-img {
    width: 100%;
  }
  .landingPage-img img {
    height: 100%;
  }
  .question-contents {
    width: 90%;
    margin: 40px auto;
  }
  .options-container button {
    font-size: 17px;
    width: 85%;
  }
  .question {
    font-size: 17px;
  }
}

@media (max-width: 500px) {
  .landingPage-contents {
    padding: 30px 20px 60px 20px;
  }
  .landingPage-text h1 {
    font-size: 30px;
  }
  .landingPage-text p {
    font-size: 16px;
  }
  .question-contents {
    width: 95%;
  }
  .options-container button {
    width: 90%;
  }
}
</style>
