<template>
  <div class="container">
    <div class="contents">
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
          v-if="currentQuestion < questions.length ? true : false"
          @click="handleNextQuestion()"
        >
          Next
        </button>
        <button
          class="submit-btn"
          v-if="currentQuestion === questions.length ? true : false"
          @click="displayResult()"
        >
          Submit
        </button>
      </div>
    </div>
  </div>
  <TotalPoints
    v-show="showResult"
    :totalPoints="points"
    :totalQuestions="questions.length"
  />
</template>

<script>
import TotalPoints from "./TotalPoints.vue";
export default {
  props: ["totalPoints", "totalQuestions"],
  name: "QuizQuestions",
  data() {
    return {
      currentQuestion: 1,
      points: 0,
      countDown: 30,
      timer: null,
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
    correctAnswer(isCorrect) {
      if (isCorrect) {
        this.points += 1;
      } else {
        this.points;
      }
    },

    displayResult() {
      this.showResult = true;
    },

    countDownTimer() {
      if (this.countDown > 0) {
        this.timer = setTimeout(() => {
          this.countDown--;
          this.countDownTimer();
        }, 1000);
      } else if (this.countDown === 0) {
        this.handleNextQuestion();
      }
    },

    handleNextQuestion() {
      clearTimeout(this.timer);
      this.currentQuestion += 1;
      this.countDown = 30;
      this.countDownTimer();
    },
  },
  mounted() {
    this.countDownTimer();
  },

  components: {
    TotalPoints,
  },
};
</script>

<style scoped>
.container {
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
.contents {
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
  width: 80%;
  margin: 70px auto;
  border-radius: 15px;
  color: #090909;
  box-shadow: 10px 10px 42px 0px rgba(0, 0, 0, 0.2);
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
  padding: 0 10px;
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
  font-weight: 600;
  width: 70%;
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
  box-shadow: inset 12rem 0rem 0rem 0rem #333;
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
@media (max-width: 960px) {
  .options-container button {
    width: 80%;
  }
}
@media (max-width: 768px) {
  .contents {
    width: 95%;
    margin: 40px auto;
  }
  .options-container button {
    font-size: 17px;
    width: 90%;
  }
  .question {
    font-size: 17px;
  }
}
</style>
