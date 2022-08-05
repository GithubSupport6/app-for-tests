<script>
import IndexComponent from './components/IndexComponent.vue'

let questionData = [
  {
    title: 'Вопрос 1',
    answers: [
      {
        title: 'Гоша',
        mask: [1,0]
      },
      {
        title: 'Гриша',
        mask: [0,1]
      },
      {
        title: 'Никто',
        mask: [0,0]
      }
    ]
  },
  {
    title: 'Вопрос 2',
    answers: [
      {
        title: 'Гоша',
        mask: [1,0]
      },
      {
        title: '2 за Гошу и 1 за Гришу',
        mask: [2,1]
      },
      {
        title: '2 за Гришу',
        mask: [0,2]
      }
    ]
  },
  {
    title: 'Вопрос 3',
    answers: [
      {
        title: 'Гриша',
        mask: [0,1]
      },
      {
        title: 'Гоша',
        mask: [1,0]
      },
      {
        title: 'Никто',
        mask: [0,0]
      }
    ]
  },
]
let questionResults = [
  {
    id: 0,
    name: "Гоша",
    image: "gosha.jpg",
    description: "Gosha description"
  },
  {
    id: 1,
    name: "Гриша",
    image: "grisha.jpg",
    description: "Grisha description"
  }
]

export default {
  name: 'App',
  components: {
    IndexComponent
  },
  data() {
    return {
      questions: questionData,
      results: questionResults
    }
  }
}
</script>

<template>
  <div class="header">
    <img id="logo" alt="logo" src="./assets/logo.jpg" width="150" height="150"> 
    <div class="header-description">
      Тест: кто ты из чята настолок
    </div>
  </div>
  
  <IndexComponent :questions="this.questions" :results="this.results"/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#logo {
  display: inline-block;
}
</style>
