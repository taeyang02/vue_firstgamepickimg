<template>
<div class="card" :class="{disable : isDisable}">
  <div class="card_inner" :class="{'is-flipped':isFliped}">
    <div class="card-face card-face front" @click="onToggleFlipCard">
      <div class="card-content"> front</div>
    </div>
    <div class="card-face card-face back" @click="onToggleFlipCard">
      <div class="card-content">
        <img v-bind:src="`${imgBackFaceUrl}`" style="width: 90px;height: 90px;padding-right: 18px" >
      </div>
    </div>
  </div>
</div>
</template>

<script>

export default {
  name: "Card",
  props:{
    card:{
      type:[String,Number,Array,Object]
    },
    imgBackFaceUrl:{
      type:String,
      required:true,
    },

  },
  data(){
    return{
      isFliped : false,
      isDisable :false,
    }
  },
  methods:{
    onToggleFlipCard(){
      console.log( this.isclick);
      if (this.isDisable) return;
     this.isFliped = !this.isFliped;
     if(this.isFliped) this.$emit("onFlip",this.card);
    },

    onFlipBackCard(){
      this.isFliped =false;
    },

    onEnableHidden(){
      this.isDisable = true;
    },


  }
}
</script>

<style scoped lang="css">
.card{
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}
.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor:  pointer;
  position: relative;
}
.card_inner.is-flipped{
  transform: rotateY(-180deg);
}
.card-face{
 position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0,0,0,0.2);
}
.front .card-content{
  background: url("../../public/images/def.png") no-repeat center center;
  background-size:90px 90px ;
  height: 100%;
  width: 100%;
}
/*.front .card-content{*/
/*  background: url("../../public/images/def.png") no-repeat center center;*/
/*  background-size:90px 90px ;*/
/*  height: 100%;*/
/*  width: 100%;*/
/*}*/

.card.disable .card_inner{
  display: none;
}
.card-face.back{
  background: var(--light);
  transform: rotateY(-150deg);
}
</style>