<template>
  <div id="app">
    <InputPanel :letters="letters" @selectLetter="selectLetter($event)"/>
    <OutputPanel :currentQuestion="currentQuestion" :currentAnswer="currentAnswer" :currentAnswerStr="currentAnswerStr" :selectedLetters="selectedLetters"/>
  </div>
</template>

<script>
import InputPanel from './components/InputPanel.vue'
import OutputPanel from './components/OutputPanel.vue'

export default {
  name: 'App',
  components: {
    InputPanel,
    OutputPanel
  },
  data(){
    return{
      letters:[
        {letter: "A", active: true},
        {letter: "B", active: true},
        {letter: "C", active: true},
        {letter: "D", active: true},
        {letter: "E", active: true},
        {letter: "F", active: true},
        {letter: "G", active: true},
        {letter: "H", active: true},
        {letter: "I", active: true},
        {letter: "J", active: true},
        {letter: "K", active: true},
        {letter: "L", active: true},
        {letter: "M", active: true},
        {letter: "N", active: true},
        {letter: "O", active: true},
        {letter: "P", active: true},
        {letter: "Q", active: true},
        {letter: "R", active: true},
        {letter: "S", active: true},
        {letter: "T", active: true},
        {letter: "U", active: true},
        {letter: "V", active: true},
        {letter: "W", active: true},
        {letter: "X", active: true},
        {letter: "Y", active: true},
        {letter: "Z", active: true}
      ],
      questions: [
        {question: "Sports Team - Cricket", answer: "Kings Eleven Punjab"},
        {question: "Name of an Organization", answer: "World Health Organization"}
      ],
      currentQuestion: "",
      currentAnswer: [],
      currentLetter: "",
      currentIndex: -1,
      currentAnswerStr: [],
      selectedLetters: []
    }
  },
  methods:{
    selectLetter(index){
      this.currentLetter = this.letters[index].letter;
      this.letters[index].active = false;
      this.selectedLetters.push(this.currentLetter);

      this.currentAnswer = this.questions[this.currentIndex].answer;

        /*for(var i=0; i<this.questions[this.currentIndex].answer.length; i++){
        if(this.currentLetter){
          if(this.questions[this.currentIndex].answer[i].toLowerCase() === this.currentLetter.toLowerCase()){
            this.currentAnswer[i] = this.questions[this.currentIndex].answer[i];
          }
          else
            this.currentAnswer[i] = (this.currentAnswer[i] === "#") ? "#" : this.currentAnswer[i];
        }
        //this.currentAnswerStr = this.currentAnswer.join('')
      }*/
    
      for(var i=0; i<this.currentAnswer.length; i++){
        if(this.currentAnswer[i].toLowerCase() === this.currentLetter.toLowerCase()){
          this.currentAnswerStr[i] = this.currentAnswer[i];
        }
        else
          this.currentAnswerStr[i] = (this.currentAnswerStr[i] === "#") ? "#" : this.currentAnswer[i];
      }

    }
  },
  created(){
    this.currentIndex = Math.random(this.questions.length).toFixed();
    this.currentQuestion = this.questions[this.currentIndex].question;
    /*for(var i=0; i<this.questions[this.currentIndex].answer.length; i++){
      this.currentAnswer[i] = "#";      
    }*/
    this.currentAnswer = this.questions[this.currentIndex].answer;
    for(var i=0; i<this.currentAnswer.length; i++){
      this.currentAnswerStr[i] = "#";      
    }
    //console.log(">>>>>> currentAnswerStr: " + this.currentAnswerStr);    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
