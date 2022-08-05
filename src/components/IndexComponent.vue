<template>
  <div class="test-panel">
  <div class="test-container" v-if="!isFinished">
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
  </div>
  <div class="result" v-if="isFinished">
    <div class="image">
      <img :src="require('@/assets/img/' + calculatedResult.image)"/>
    </div>
    <div class="name">
      {{calculatedResult.name}}
    </div>
    <div class="description">
      {{calculatedResult.description}}
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
    calculatedResult() {
      let max = Math.max(...this.currentResults)
      let indexesOfWinners = [];
      for (let i = 0;i<this.currentResults.length;i++){
        if (this.currentResults[i] == max){
          indexesOfWinners.push(i)
        }
      }
      let winnersCount = indexesOfWinners.length
      let winnerIndex = winnersCount > 1 ?
        Math.floor(Math.random() * indexesOfWinners.length) :
        indexesOfWinners[0]
      return this.results[winnerIndex]
    },
    getImgUrl(image){
      return require("../assets/img/" + image)
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
