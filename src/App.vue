<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>

      <div
        class="quiz-main"
        v-for="(element, index) in questions.slice(a, b)"
        :key="index"
        v-show="quiz"
      >
        <div class="box-question">
          <h2>PREGUNTAS {{ b }}/{{ questions.length }}</h2>
          <p>{{ element.question }}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li
              v-for="(item, index) in element.suggestions"
              :key="index"
              :class="select ? check(item) : ''"
              @click="selectResponse(item)"
            >
              {{ item.suggestion }}
            </li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show"></div>
      <h2>Your score is</h2>
      <h2>{{ score }}/{{ questions.length }}</h2>
      <div class="btn-restart">
        <button @click="restartQuiz">Restart</button>
      </div>

      <div class="quiz-footer">
        <div class="box-button">
          <button @click="skipQuestion">Skip</button>
          <button @click="nextQuestion">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      questions: [
        {
          question: "pregunta?",
          suggestions: [
            { suggestion: "alternativa", correct: true },
            { suggestion: "alternativa" },
            { suggestion: "alternativa" },
          ],
        },
        {
          question: "pregunta?",
          suggestions: [
            { suggestion: "alternativa" },
            { suggestion: "alternativa", correct: true },
            { suggestion: "alternativa" },
          ],
        },
        {
          question: "pregunta?",
          suggestions: [
            { suggestion: "alternativa", correct: true},
            { suggestion: "alternativa" },
            { suggestion: "alternativa",  },
          ],
        },
        {
          question: "pregunta?",
          suggestions: [
            { suggestion: "alternativa" },
            { suggestion: "alternativa" },
            { suggestion: "alternativa", correct: true },
          ],
        },
        {
          question: "pregunta?",
          suggestions: [
            { suggestion: "alternativa" },
            { suggestion: "alternativa", correct: true },
            { suggestion: "alternativa" },
          ],
        },
      ],

      a: 0,
      b: 1,
      select: false,
      score: 0,
      quiz: true,
      score_show: false,
      next: false,
    };
  },

  methods: {
    selectResponse(e) {
      this.select = true;
      this.next = true;
      if (e.correct) {
        this.score++;
      }
    },

    check(status) {
      if (status.correct) {
        return "correct";
      } else {
        return "incorrect";
      }
    },
    nextQuestion() {
      if (!this.next) {
        return;
      }

      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
        this.select = false;
        this.next = false;
      }
    },

    skipQuestion() {
      if (this.next) {
        return;
      }

      if (this.questions.length - 1 == this.a) {
        this.score_show = true;
        this.quiz = false;
      } else {
        this.a++;
        this.b++;
      }
    },

    restartQuiz() {
      Object.assign(this.$data, this.$options.data()); //TODO: reset data
    },
  },
};
</script>
