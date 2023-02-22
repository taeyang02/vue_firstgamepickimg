<template>
<div class="screen">
  <h1>GIRL MEMORIES</h1>
  <h3>Select mode to start game</h3>
  <div class="action">
    <button @click="onStart(16)">
      <span>4x4</span>
      <span>Easy</span>
    </button>
    <button @click="onStart(36)">
      <span>6x6</span>
      <span>Normal</span>
    </button>
    <button @click="onStart(64)">
      <span>8x8</span>
      <span>Hard</span>
    </button>
    <button @click="onStart(100)">
      <span>10x10</span>
      <span>Very Hard</span>
    </button>
  </div>
</div>
</template>

<script>
export default {
  name: "MainScreen",
  methods:{
    onStart(totalOfBlocks){
      this.$emit("onStart",{totalOfBlocks})
    }
  }
}
</script>

<style scoped>
.screen{
  position: absolute;
  top: 25%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.action button {
  background-color: #fff;
  border: 2px solid #000;
  color: #000;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 5px;
}

.action button span:first-child {
  font-weight: bold;
}

.action button span:last-child {
  font-size: 12px;
  font-style: italic;
}


</style>