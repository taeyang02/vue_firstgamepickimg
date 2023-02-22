<template>
  <div class="screen">
<h1>Congratulation</h1>
 <p>{{Math.round(timer/1000)}} Seconds</p>
  <button @click="onStartAgain()">Start Again</button>
  </div>
</template>

<script>
export default {
  name: "ResultScreen",
  props:{
    timer:{
      type : Number,
      required : true
    }
  },
  methods:{
    onStartAgain(){
      this.$emit("onStartAgain");
    }
  }
}
</script>

<style scoped>
</style>