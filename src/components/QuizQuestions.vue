<template>
  <div class="wrapper">
    <!-- welcome page -->
    <div v-show="!startQuiz" class="landingPage">
      <div class="landingPage-contents">
        <div class="landingPage-img">
          <img src="../assets/img/icon6.png" alt="icon" />
        </div>
        <div class="landingPage-text">
          <h1>QUIZ APP</h1>
          <p>
            You are presented with questions and four options, you have 30
            seconds to answer each question after which you will be
            automatically moved to the next question. Failure to select an
            answer within the time limit will result in a loss of points. At the
            end of the quiz, your total score will be displayed. Good luck!!
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
  </div>
</template>

<script>
import TotalPoints from "./TotalPoints.vue";
import QuestionData from "../assets/questionData.json";

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
      questions: QuestionData,
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

    displayResult() {
      this.showResult = true;
      this.countDown = 1;
    },
  },

  components: {
    TotalPoints,
  },
};
</script>

<style scoped>
@import "../assets/quizQuestionStyle.css";
</style>
