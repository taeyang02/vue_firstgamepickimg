<template>
  <div class="screen">
    <h1 style="margin: auto;">TaeYang_Games</h1>
    <div class="screen_inner">
  <card-flip v-for="(card, index) in cardsContext"
             :key="index"
             :imgBackFaceUrl="`/images/${card}.jpg`"
             :card="{index,value:card}"
             :ref="`card-${index}`"
             @onFlip="checkRule($event)"
  />
    </div>
  </div>


<!--  <test ref="hellox"/>-->
</template>

<script>
import CardFlip from "@/components/Card.vue";
import Test from "@/components/Test.vue";
export default {
  name: "InteractScreen",
  props:{
    cardsContext: {
      type: Array,
      default : function (){
        return [];
      },
    }
  },
  components:{
    CardFlip,
    Test,
  },
  data(){
    return{
      rules:[],
    }
  },
  methods:{
    checkRule(card){
      if(this.rules.length === 2) return false;
      this.rules.push(card);
      if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
        setTimeout(()=>{
          this.$refs[`card-${this.rules[0].index}`][0].onEnableHidden();
          this.$refs[`card-${this.rules[1].index}`][0].onEnableHidden();
          this.rules =[];
        },800)
        const hiddenElement = document.querySelectorAll(".screen .card.disable");
        console.log(hiddenElement);

        if (hiddenElement && hiddenElement.length == this.cardsContext.length-2){
          setTimeout(()=>{this.$emit("onFinish")},920);
        }
      }
      if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value){
        setTimeout(()=>{
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules =[];
        },800)
      }else {
        return false;
      }
    }
  }
}
</script>

<style scoped>
.screen{
  width:100%;
  height:100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}

.screen_inner{
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>