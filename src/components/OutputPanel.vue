<template>
  <div id="OutputPanel" class="OutputPanel">
    <div>
      <h3>{{currentQuestion}}</h3>
      <!-- <h3>{{selectedLetters}}</h3> -->
      <div class="answer-panel">
        <div v-for="(letter, index) in currentAnswerStr" 
          :key="index"
          class="answer-span-empty"
          :class="hideBox(letter, index)"
          >
          <!-- <div v-html="letter" :class="{hash: letter === '#'}"/> -->
          <!-- <p :class="{hash: letter === '#'}"> {{ letter }}</p> -->
          <!-- <span v-html="letter" :class="hideLetters(letter)"> {{ letter | capitalize }}</span> -->
          <span :class="hideLetters(letter)"> {{ letter | capitalize }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'OutputPanel',
  props: [
    "currentQuestion",
    "currentAnswerStr",
    "currentAnswer",
    "selectedLetters"
  ],
  components: {
  },
  methods: {
    hideLetters(letter){
      //console.log(this.selectedLetters.includes(letter))
      if(!this.selectedLetters.map(x => x.toLowerCase()).includes(letter.toLowerCase()))
        return "hash";
      else
        return "display-letter"
    },
    hideBox(letter, index){
      //console.log(index)
      //console.log(this.selectedLetters.includes(letter))
      if(this.currentAnswer[index] === " "){
        return "hideBox";
      }
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
  /*display:inline-block;*/
  margin:60px auto 45px;
  /* background-color:#5597b4; */
  background-color: #F39721;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 950px;
  height: 300px;
  border-radius: 2%;
}
.answer-panel{
  /* padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 900px;
  height: 200px; */

  /* display: flex; */
  display: grid;
  grid: 55px / auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto auto ;
  grid-gap: 0px;
  /* background-color: #2196F3; */
  /* background-color: #F39721; */
  padding: 10px;
  /* color: lightgreen; */
  color: white;
  font-size: 50px;line-height: 10px;letter-spacing: 0px;font-weight: 700;
}
.answer-span-empty{
  /* display: table-cell;
  border: 1px solid linen;
  border-radius: 30%;
  width: 20px;
  padding-left: 10px;
  padding-right: 10px;
  padding-top: 10px;
  padding-bottom: 10px;
  margin: 5px; */

  /* background-color: #f1f1f1;
  width: 100px;
  margin: 10px;
  text-align: center;
  line-height: 0px;
  font-size: 20px; */

  /* background-color: rgba(255, 255, 255, 0.8); */
  /* background-color: #f1f1f1; */
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
  border-radius: 30%;
  box-shadow: 0 2px 8px rgb(202, 126, 26) inset;
  height: 10px;
  width: 50px;
  background-color: rgb(97, 225, 97);
}
.space{
  padding: 2px !important;
}
.hash{
  /* color: #f1f1f1; */
  /* color: #f1f1f1; */
  color: #F39721;
  opacity: 0%;
}
.display-letter{
  display: block;
}
.hideBox{
  /* background-color: #2196F3; */
  box-shadow: 0 2px 8px rgb(202, 126, 26) inset;
  background-color: #F39721;
  /* box-shadow: none; */
}
</style>
