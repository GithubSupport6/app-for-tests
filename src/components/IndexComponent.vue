<template>
  <div class="test-panel">
  <div class="container">
    <div class = "header">
      {{currentQuestion.title}}
    </div>
    <div class="questions">
      <ul>
        <li v-for="answer in currentAnswers" v-bind:key="answer">
          <input type='radio' name="answersRadio" v-on:click="selectedAnswer = answer">
          <label> {{answer.title}}</label>
        </li>
      </ul>
    </div>
    <div class="submit">
      <input type="submit" value="Да!" v-on:click="nextQuestion(selectedAnswer)">
    </div>
    <div class="result" v-if="isFinished">
      {{this.calculateResult.name}}
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: [
    'questions',
    'results'
  ],
  data() {
    return {
      currentIndex: 0,
      isFinished: false,
      currentResults: Array(this.results.length).fill(0),
      selectedAnswer: null
    }
  },
  computed: {
    currentQuestion(){
      return this.questions[this.currentIndex]
    },
    currentAnswers(){
      return this.questions[this.currentIndex].answers
    },
    calculateResult() {
      let max = Math.max(this.currentResults)
      let indexesOfWinners = [];
      for (let i = 0;i<this.currentResults;i++){
        if (this.currentResults[i] == max){
          indexesOfWinners+=i
        }
      }
      let winnerIndex = Math.random() + indexesOfWinners.length
      return this.results[winnerIndex]
    }
  },
  methods: {
    calculateStep(mask){
      for (let i = 0; i<mask.length;i++){
        this.currentResults[i] += mask[i]
      }
    },
    nextQuestion(answer) {
      this.calculateStep(answer.mask)
      if (this.currentIndex < this.questions.length - 1) {  
        this.currentIndex++
      }   
      else
        this.isFinished = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
