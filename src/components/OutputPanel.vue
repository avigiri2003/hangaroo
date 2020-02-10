<template>
  <div id="OutputPanel" class="OutputPanel">
    <div>
      <h3>{{currentQuestion}}</h3>
      <!-- <p style="display: none">{{currentLetter}}</p> -->
      <div class="answer-panel">
        <span v-for="(letter, index) in currentAnswerStr" 
          :key="index"
          class="answer-span-empty"
          >
          <!-- {{index}}{{letter}} -->
          <!-- <span v-html="letter" :class="{hash: letter === '#'}"/> -->
          <p :class="{hash: letter === '#'}"> {{ letter }}</p>
        </span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'OutputPanel',
  props: [
    "currentLetter",
    "currentQuestion",
    "currentAnswerStr"
  ],
  components: {
    
  },
  data(){
    return{
    }
  },
  methods:{
  }
//   computed: {
//     answerArray(){
//       let answerArray_1 = [...this.currentAnswer];
// console.log(">>> currentAnswer: " + this.currentAnswer);      
//       return answerArray_1;
//     }
//   }
}
</script>

<style scoped>
.OutputPanel{
  /*display:inline-block;*/
  margin:60px auto 45px;
  background-color:#5597b4;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 950px;
  height: 200px;
}
.answer-panel{
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 900px;
  height: 200px;
}
.answer-span-empty{
  display: table-cell;
  border: 1px solid linen;
  width: 20px;
  padding-left: 10px;
  padding-right: 10px;
  padding-top: 10px;
  padding-bottom: 10px;
}
.space{
  padding: 2px !important;
}
.hash{
  display: none;
}
</style>
