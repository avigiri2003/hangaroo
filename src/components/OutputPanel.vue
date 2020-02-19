<template>
  <div id="OutputPanel" class="OutputPanel" :class="blink()">
    <div>
      <h3>{{currentQuestion | capitalize}}</h3>
      <div class="answer-panel" :class="{'newQes': newQuestion === true}">
        <div v-for="(letter, index) in currentAnswerStr" 
          :key="index"
          class="answer-span-empty"
          :class="hideBox(letter, index)"
          >
          <span :class="hideLetters(letter)"> {{ letter | capitalize }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'OutputPanel',
  data(){
    return{
      newQuestion: false
    }
  },
  props: [
    "currentQuestion",
    "currentAnswerStr",
    "currentAnswer",
    "selectedLetters",
    "answerMatch"
  ],
  components: {
  },
  watch:{
    selectedLetters: {
      immediate: true,
      handler(){
        if(this.selectedLetters.length === 0)
          this.newQuestion = true;
        else
          this.newQuestion = false;
      }
    }
  },
  methods: {
    hideLetters(letter){
      if(!this.selectedLetters.map(x => x.toLowerCase()).includes(letter.toLowerCase()))
        return "hash";
      else
        return "display-letter"
    },
    hideBox(letter, index){
      if(this.currentAnswerStr[index] === " ")
        return "hideBox";
      else
        return "showBox";
    },
    blink(){
      if(this.answerMatch)
        return "blink";
      else
        return "";
    }
  },
  filters:{
    capitalize(val){
      return val.toUpperCase();
    }
  }
}
</script>

<style scoped>

* {
  font-family: Consolas;
}
.OutputPanel{
  margin:30px auto 20px;
  background-color: #F39721;
  padding-top: 5px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 950px;
  height: 280px;
  border-radius: 25px;
  border: 5px solid yellow;
}
.blink{
  animation: blinking linear 0.5s infinite;
}
@keyframes blinking {
  from,
  49.9% {
    opacity: 0;
  }
  50%,
  to {
    opacity: 1;
  }
}

h3{
  font-size: 25px;
  color: white;
  margin:-25px auto 20px;
  background-color: #33AAD9E6;
  padding-top: 5px;
  padding-bottom: 5px;
  padding-left: 10px;
  padding-right: 10px;
  width: 800px;
  height: 25px;
  border: 2px solid yellow;
  border-radius: 15px;
  line-height: 1;
}
.answer-panel{
  display: grid;
  grid: 50px / auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto ;
  grid-gap: 5px;
  padding: 10px;
  color: white;
  font-size: 50px;line-height: 10px;letter-spacing: 0px;font-weight: 700;
}
.answer-span-empty{
  text-align: center;
  padding: 20px 0;
  font-size: 40px;
  border-radius: 30%;
  box-shadow: 0 2px 8px rgb(202, 126, 26) inset;
  height: 10px;
  width: 50px;
  background-color: rgb(97, 225, 97);
}
.showBox {
  animation-name: example;
  animation-duration: 1s;
}
@keyframes example {
  0%   {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:0px;}
  10%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:5px;}
  20%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:10px;}
  30%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:15px;}
  40%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:20px;}
  50%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:25px;}
  60%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:30px;}
  70%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:35px;}
  80%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:40px;}
  90%  {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:45px;}
  100% {box-shadow: 0 2px 8px rgb(202, 126, 26) inset; background-color:rgb(97, 225, 97); width:50px;}
}
.space{
  padding: 2px !important;
}
.hash{
  color: #F39721;
  opacity: 0;
}
.display-letter{
  display: block;
}
.hideBox{
  box-shadow: 0 2px 8px rgb(202, 126, 26) inset;
  background-color: #F39721;
}
</style>
