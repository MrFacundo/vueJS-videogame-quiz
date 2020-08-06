<template>
  <div id="app">
    <Header
      :index="index"
      :progress="progress"
    />
    <div class="container">
      <Results 
        v-if="score_show"
        :numCorrect="numCorrect"
        :numTotal="numTotal"
        :nextQuiz="nextQuiz"
      /> 
    </div>
      <b-container class="bv-example-row">
        <b-row >
          <b-col xs="12" md="12" lg="6" offset-lg="3"	>
            <QuestionBox
              v-if="questions.length && !score_show"
              :currentQuestion="questions[index]"
              :next="next"
              :increment="increment"
            />
          </b-col>
        </b-row>
      </b-container>
  </div>
</template>

<script>
import QuestionBox from './components/QuestionBox.vue'
import Header from './components/Header.vue'
import Results from './components/Results.vue'


export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Results
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      score_show: false,
      progress: 0
    }
  },
  methods: {
    next() {
      this.progress = this.progress + 10;
      if (this.index == 9) {
        this.score_show = true;
      } else {
          this.index++
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
          this.numCorrect++
      }
      this.numTotal++
    },
    nextQuiz: function() {
      this.index = 0;
      this.numCorrect = 0;
      this.numTotal = 0;
      this.getQuizQuestions();
      this.score_show = false;
      this.progress= 0
    },
    getQuizQuestions: function() {
      fetch('https://opentdb.com/api.php?amount=10&category=15&difficulty=easy&type=multiple&encode=url3986', {
      method: 'get'
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results
      })
    }
  },
  mounted: function() {
    this.getQuizQuestions();
  }
}
</script>

<style>
#app {
  font-family: 'Press Start 2P', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-image: url('assets/wonder-boy1-large.jpg');
  background-position: calc(100% - 158px) center;

}

</style>

