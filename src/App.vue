<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import ResultScreen from "@/components/ResultScreen.vue";
import {shuffled} from "./ultil/array"
export default {
  name:"App",
  components:{
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data(){
    return{
      setting :{
        totalOfBlock:0,
        cardsContext:[],
        startedAt: null,
      },
      statusMatch : "default",
      timer : 0,
    }
  },
  methods:{
    onHandleBeforeStart(config){
      // console.log("start ...",config)
      this.setting.totalOfBlock = config.totalOfBlocks;
      const fisrtArr = Array.from({length: this.setting.totalOfBlock / 2},(_,i)=>i+1);
      const  secondCard = [...fisrtArr];
      const  cards = [...secondCard,...fisrtArr];
      this.setting.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
      this.setting.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onGetResult(){
      this.timer = new Date().getTime() - this.setting.startedAt;
      this.statusMatch = 'result';
    },

  }
}
</script>

<template>
  <div>
  <MainScreen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)"></MainScreen>
  <InteractScreen v-if="statusMatch === 'match'" :cardsContext="setting.cardsContext" @onFinish="onGetResult()"></InteractScreen>
  <ResultScreen v-if="statusMatch === 'result'" :timer="timer" @onStartAgain="this.statusMatch = 'default'"></ResultScreen>
  </div>
</template>

<style>

</style>
