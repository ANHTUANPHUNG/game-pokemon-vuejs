<template>
  <div>
    <main-screen 
    v-if="statusMatch === 'default'"  
    @onStart = handleTransitionPage($event) />
  <interact-screen  
  v-if="statusMatch === 'match'"
  :cardsContext = "settings.cardsContext"
  @onFinish = "onGetResult"
  />
  <result-screen
  v-if="statusMatch === 'result'"
  :timer="timer"
  @onStartAgain="statusMatch= 'default'"
  />
  </div>
</template>

<script>
import MainScreen from './components/MainScreen.vue'; 
import InteractScreen from './components/InteractScreen.vue';
import {shuffled} from './utils/array';
import ResultScreen from './components/ResultScreen.vue';
export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data () {
  return {
    settings:{
      totalOfBlocks:0,
      cardsContext:[],
      startedAt: null,
    },
    statusMatch:"default",
    timer: 0
  }
  },
  
  
methods: {
    handleTransitionPage(value){
      const cards = Array.from({
        length: value.totalOfBlocks/2
      }, (_,i)=> i+1)
      const listImage = [...cards,...cards]
      this.settings.cardsContext= shuffled(shuffled(shuffled(listImage)))
      this.statusMatch = "match"
      this.settings.startedAt = new Date().getTime()
      console.log(this.startedAt);
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch ="result";
     }
  }
}
</script>
