<template>
  <div id="app">
    <div class="wrongAns" :class="{blink: wrongAnswerCount === 4}">
      <span :class="{wrongAnsOne: wrongAnswerCount >= 1}">X</span>
      <span :class="{wrongAnsTwo: wrongAnswerCount >= 2}">X</span>
      <span :class="{wrongAnsThree: wrongAnswerCount >= 3}">X</span>
      <span :class="{wrongAnsFour: wrongAnswerCount >= 4}">X</span>
    </div>
    <InputPanel 
      v-if="currentQuestion.length > 1"
      :letters="letters" @selectLetter="selectLetter($event)"
      :answerMatch="answerMatch"/>
    <OutputPanel 
      v-if="currentQuestion.length > 1"
      :currentQuestion="currentQuestion" 
      :currentAnswer="currentAnswer" 
      :currentAnswerStr="currentAnswerStr" 
      :selectedLetters="selectedLetters"
      :answerMatch="answerMatch"/>
    
    <Footer/>
  </div>
</template>

<script>
import InputPanel from './components/InputPanel.vue'
import OutputPanel from './components/OutputPanel.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    InputPanel,
    OutputPanel,
    Footer
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
        {question: "Name of an Organization", answer: "World Health Organization"},
        {question: "Movies - Action Films", answer: "Planet Of The Apes"},
        {question: "Science And Technology - Computer Terms, Parts and Things", answer: "HYPERTEXT MARKUP LANGUAGE"},
        {question: "Popular Places and Landmarks", answer: "ALHAMBRA PALACE"},
        {question: "Popular Places and Landmarks", answer: "AMAZON RAINFOREST"},
        {question: "Popular Places and Landmarks", answer: "DISNEY WORLD"},
        {question: "Popular Places and Landmarks", answer: "DISNEYLAND"},
        {question: "Popular Places and Landmarks", answer: "HANGING GARDENS OF BABYLON"},
        {question: "Popular Places and Landmarks", answer: "LOST CITY OF ATLANTIS"},
        {question: "Popular Places and Landmarks", answer: "STATUE OF LIBERTY"},
        {question: "Popular Places and Landmarks", answer: "THE PENTAGON"},
        {question: "Popular Places and Landmarks", answer: "YELLOWSTONE NATIONAL PARK"},
        {question: "Comman Phrases and Slogans", answer: "A COWARD DIES A HUNDRED DEATHS"},
        {question: "Comman Phrases and Slogans", answer: "A FRIEND IN NEED IS A FRIEND INDEED"},
        {question: "Comman Phrases and Slogans", answer: "A MAN IS KNOWN BY THE COMPANY HE KEEPS"},
        {question: "Comman Phrases and Slogans", answer: "ALL IS WELL THAT ENDS WELL"},
        {question: "Comman Phrases and Slogans", answer: "BETTER LATE THAN NEVER"},
        {question: "Comman Phrases and Slogans", answer: "BETTER THE DEVIL YOU KNOW THAN THE DEVIL YOU DON'T KNOW"},
        {question: "Comman Phrases and Slogans", answer: "CLOTHES DONT MAKE THE MAN"},
        {question: "Comman Phrases and Slogans", answer: "ELEVENTH HOUR"},
        {question: "Comman Phrases and Slogans", answer: "NECESSITY IS THE MOTHER OF INVENTION"},
        {question: "Movies - Animation Films", answer: "ALICE IN WONDERLAND"},
        {question: "Movies - Animation Films", answer: "ICE AGE"},
        {question: "Movies - Animation Films", answer: "SHREK"},
        {question: "Movies - Animation Films", answer: "THE JUNGLE BOOK"},
        {question: "Movies - Animation Films", answer: "THE LION KING"},
        {question: "Movies - Animation Films", answer: "TOY STORY"},
        {question: "Movies - Horror Films", answer: "FRANKENSTEIN"},
        {question: "Movies - Horror Films", answer: "JAWS"},
        {question: "Movies - Horror Films", answer: "THE EXORCIST"},
        {question: "Movies - Horror Films", answer: "THE RING"},
        {question: "Movies - Horror Films", answer: "WAIT UNTIL DARK"},
        {question: "Animals and Plants", answer: "AFRICAN WILD DOG"},
        {question: "Animals and Plants", answer: "AMERICAN BULLDOG"},
        {question: "Animals and Plants", answer: "AUSTRALIAN SHEPHERD DOG"},
        {question: "Animals and Plants", answer: "ENGLISH COONHOUND"},
        {question: "Animals and Plants", answer: "PAPILLON"},
        {question: "Holidays Around The World", answer: "BAISAKHI"},
        {question: "Holidays Around The World", answer: "DIWALI"},
        {question: "Holidays Around The World", answer: "MEMORIAL DAY"},
        {question: "Holidays Around The World", answer: "PASSOVER"},
        {question: "Holidays Around The World", answer: "REMEMBRANCE DAY"},
        {question: "Holidays Around The World", answer: "SANTA LUCIA DAY"},
        {question: "Holidays Around The World", answer: "SPRING BREAK"},
        {question: "Holidays Around The World", answer: "VICTORIA DAY"},
        {question: "Significant Historic Events", answer: "BATTLE OF BUNKER HILL"},
        {question: "Significant Historic Events", answer: "BOSTON TEA PARTY"},
        {question: "Significant Historic Events", answer: "CALIFORNIA GOLD RUSH"},
        {question: "Significant Historic Events", answer: "CIVIL WAR"},
        {question: "Significant Historic Events", answer: "GREAT CHICAGO FIRE"},
        {question: "Significant Historic Events", answer: "PERSIAN GULF WAR"},
        {question: "Significant Historic Events", answer: "RUSSIAN REVOLUTION"},
        {question: "Significant Historic Events", answer: "SPANISH AMERICAN WAR"},
        {question: "Significant Historic Events", answer: "VIETNAM WAR"},
        {question: "Significant Historic Events", answer: "WOODSTOCK"}
        
      ],
      currentQuestion: "",
      currentAnswer: [],
      currentLetter: "",
      currentIndex: -1,
      currentAnswerStr: [],
      selectedLetters: [],
      answerMatch: false,
      wrongAnswerCount: 0
    }
  },
  methods:{
    selectLetter(index){

      if(this.wrongAnswerCount === 4){
        return;
      }

      this.currentLetter = this.letters[index].letter;
      this.letters[index].active = false;
      // setTimeout(function(){
      //   document.querySelector(".inputpanel_nav_selected").setAttribute("style", "opacity: 0.7 !important");
      // }, 100);
      this.selectedLetters.push(this.currentLetter);

      //Commented below line on 15.02
      //this.currentAnswer = this.questions[this.currentIndex].answer;
    
      var letterMatch = false;
      for(var i=0; i<this.currentAnswer.length; i++){
        if(this.currentAnswer[i].toLowerCase() === this.currentLetter.toLowerCase()){
          this.currentAnswerStr[i] = this.currentAnswer[i];
          letterMatch = true;
        }
        else
          this.currentAnswerStr[i] = (this.currentAnswerStr[i] === "#") ? "#" : this.currentAnswer[i];
      }
      
      //Check for answer match...
      if(JSON.stringify(this.currentAnswer)==JSON.stringify(this.currentAnswerStr)){
        this.answerMatch = true;
      }

      if(this.answerMatch){
        setTimeout(this.nextQ, 3000);
      }

      if(!letterMatch){
        this.wrongAnswerCount++;
        this.playSound("wrong");
      }

      if(this.wrongAnswerCount === 4){
        this.currentAnswerStr = [];
        setTimeout(this.nextQ, 3000);
      }

    },

    getCenterIndex(str){
      let centerIndex = Math.floor((17 - str.length) / 2);
      // console.log(">>> in getCenterIndex. Str: " + str + ", centerIndex: " + centerIndex);
      return centerIndex;
    },

    nextQ(){
      this.answerMatch = false;
      this.selectedLetters = [];
      this.currentLetter = "";
      this.letters.forEach(function(item){
        item.active = true;
      });
      this.wrongAnswerCount = 0;

      // this.currentIndex = Math.random(this.questions.length + 2).toFixed();
      this.currentIndex = Math.floor(Math.random() * this.questions.length);
      this.currentQuestion = this.questions[this.currentIndex].question;
      this.currentAnswer = this.questions[this.currentIndex].answer;

      var lines = [""];
      var lineNum = 0;
      // var newString = "This is a difficult problem";
      // var newArr = newString.split(" "); 
      var newArr = this.currentAnswer.split(" ");

      //------------- STEP 1 -------------
      for(var a=0; a<newArr.length; a++){
        if( (lines[lineNum].length + newArr[a].length + 1) <=16 ){
          if(a===0)
            lines[lineNum] = newArr[a];
          else
            lines[lineNum] = lines[lineNum] + " " + newArr[a];
        }
        else{
          lines[++lineNum] = newArr[a];
        }
      // console.log(">>> a= " + a + ", lineNum: " + lineNum + "lines: " + lines);
      }

      //------------- STEP 2 -------------
      var len = lines.length;
      for(var b=0; b < len; b++){
        var ci = this.getCenterIndex(lines[b]);
        console.log(">>> lines[b]=" + lines[b] + ", ci: " + ci);
        for(var c=0; c < ci; c++){
          lines[b] = " " + lines[b];
          lines[b] = lines[b] + " ";
        }
        if(lines[b].length < 17)
          lines[b] = lines[b] + " ";
      console.log(">>> lines[b]=" + lines[b] + ", length: " + lines[b].length);
      }

      //------------- STEP 3 -------------
      len = lines.length;
      var d;
      var tempLine_1 = "";
      var tempLine_2 = "";
      // console.log(">>> STEP 3 len: " + len);
      switch(len){
        case 1:
          tempLine_1 = lines[0];
          lines[0] = "";
          lines[1] = "";
          lines[2] = "";
          lines[3] = "";
          for(d=0; d < 17; d++){
            lines[0] = lines[0] + " ";
            lines[2] = lines[2] + " ";
            lines[3] = lines[3] + " ";
          }
          lines[1] = tempLine_1;
          break;

        case 2:
          tempLine_1 = lines[0];
          tempLine_2 = lines[1];
          lines[0] = "";
          lines[1] = "";
          lines[2] = "";
          lines[3] = "";
          for(d=0; d < 17; d++){
            lines[0] = lines[0] + " ";
            lines[3] = lines[3] + " ";
          }
          lines[1] = tempLine_1;
          lines[2] = tempLine_2;
          break;

        case 3:
          lines[3] = "";
          for(d=0; d < 17; d++){
            lines[3] = lines[3] + " ";
          }
          break;

        case 4:
          //nothing to do
          break;
      }
      console.log(">>> lines=" + lines);

      //------------- STEP 4 -------------
      var finalStr = "";
      for(var e=0; e < lines.length; e++){
        finalStr = finalStr + lines[e];
      }
      console.log(">>> finalStr: " + finalStr);

      this.currentAnswer = [];
      for(var j=0; j<finalStr.length; j++){
        if(finalStr[j] === " "){
          this.currentAnswerStr[j] = " ";
          this.currentAnswer[j] = " ";
        }
        else{
          this.currentAnswerStr[j] = "#";
          this.currentAnswer[j] = finalStr[j];
        }
      }
      console.log(">>> this.currentAnswerStr: " + this.currentAnswerStr);
      console.log(">>> this.currentAnswer: " + this.currentAnswer);
    },

    playSound(sound) {
      if(sound) {
        if(sound === "wrong"){
          var audio = new Audio("http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3");
          //  var audio = new Audio("./assets/sample_wav.wav");
          //  audio.type = 'audio/wav';
          audio.play();
          //audio.pause();
          //audio.currentTime = 0;
         }
      }
        
    }


  },
  created(){
    this.nextQ();
  }

  // ,created_old_2(){
  //    //let newString = "This is a difficult problem";
  //   var newString = "World Health Organization";
  //   var newArr = newString.split(" "); 
  //   var yourVar = 0;
  //   var resultStr = [];
  //   console.log("newArr: " + newArr);
  //   for(var s=0; s < newArr.length; s++){
  //     var vbc = "";
  //     for(var oops=0; oops<resultStr.length; oops++)
  //       vbc = vbc + resultStr[oops];
  //     console.log("vbc: " + vbc);
  //     //if(s===0)
  //       //resultStr[s] = newArr[s];
  //     //else
  //       //resultStr = resultStr.concat(newArr[s]);
  //     if(s !== 0)
  //       resultStr.push(" ");
  //     for(var o=0; o<newArr[s].length; o++)
  //       resultStr.push(newArr[s][o]);
  //     console.log("resultStr: " + resultStr + ", resultStr length: " + resultStr.length);

  //     if(resultStr.length <=16){
  //     console.log(">> IF");
  //       yourVar = this.getCenterIndex(resultStr);
  //       for(var t=0; t<yourVar; t++){
  //         resultStr.unshift(" ");
  //         //resultStr.pop();
  //       }
  //     }
  //     else{
  //       yourVar = this.getCenterIndex(newArr[s]);
  //       console.log(">> ELSE" + ", newArr[s]: " + newArr[s] + ", yourVar: " + yourVar + ", vbc.length: " + vbc.length);
  //       for(var d=0; d<yourVar + (17-(vbc.length + newArr[s].length)); d++)
  //         resultStr.splice(vbc.length, 0, " ");
  //     }
  //   console.log(">> s= " + s + ", resultStr: " + resultStr);
  //   }
  //   console.log(">> Final resultStr: " + resultStr + ", length: " +  resultStr.length);

  //   for(var h=0; h<resultStr.length; h++){
  //     if(resultStr[h] === " ")
  //       this.currentAnswerStr[h] = " ";      
  //     else
  //       this.currentAnswerStr[h] = "#";      
  //   }
  // }

  // ,created_old(){
  //   this.currentIndex = Math.random(this.questions.length).toFixed();
  //   this.currentQuestion = this.questions[this.currentIndex].question;
  //   /*for(var i=0; i<this.questions[this.currentIndex].answer.length; i++){
  //     this.currentAnswer[i] = "#";      
  //   }*/
  //   this.currentAnswer = this.questions[this.currentIndex].answer;
  //   // for(var i=0; i<this.currentAnswer.length; i++){
  //   //   this.currentAnswerStr[i] = "#";      
  //   // }

  //   for(var i=0; i<68; i++){
  //      this.currentAnswerStr[i] = " ";      
  //   }

  //   // for(var j=20; j<20+this.currentAnswer.length; j++){
  //   //   if(this.currentAnswer[j-20] === " ")
  //   //     this.currentAnswerStr[j] = " ";      
  //   //   else
  //   //     this.currentAnswerStr[j] = "#";      
  //   // }

  //   for(var j=0; j<this.currentAnswer.length; j++){
  //     if(this.currentAnswer[j] === " ")
  //       this.currentAnswerStr[j] = " ";      
  //     else
  //       this.currentAnswerStr[j] = "#";      
  //   }

    
  //   let something = this.currentAnswer.split(" ");
  //   let counter = 0;
  //   let start = 20;

  //   console.log(">>> " + something, counter, start);

  //   let myVar = 0;
  //   let tempStr = "";
  //   for(var k=0; k<something.length; k++){
  //     tempStr = tempStr + " " + something[k];
  //     myVar = Math.round((17 - myVar - tempStr.length) / 2);
  //     console.log(">>> myVar: " + myVar + " tempStr: " + tempStr);
      
  //     for(var m=0; m<myVar; m++){
  //       this.currentAnswerStr.unshift(" ");
  //       this.currentAnswerStr.pop();
  //     }
  //   }

  //   /*
  //   // for(var k=0; k<start; k++){
  //   //   this.currentAnswerStr.unshift(" ");
  //   //   if(this.currentAnswerStr.length > 68)
  //   //     this.currentAnswerStr.pop();
  //   // }

  //   let myVar = Math.floor((68 - this.currentAnswer.length) / 2);
  //   console.log(">>> myVar: " + myVar);
  //   for(var k=0; k<myVar; k++){
  //     this.currentAnswerStr.unshift(" ");
  //     this.currentAnswerStr.pop();
  //   }

  //   var ix = this.currentAnswerStr.indexOf("#");
  //   for(var z=0; z<myVar; z++){

  //   }

  //   // while(counter < something.length){
  //   //   if(counter > 0 && something[counter].length >=16){
  //   //     start = something[counter].length + 1;
  //   //     counter++;
  //   //     continue;
  //   //   }
  //   //   else{
  //   //     for(var k=0; k<start; k++){
  //   //     this.currentAnswerStr.unshift(" ");
  //   //     if(this.currentAnswerStr.length > 68)
  //   //       this.currentAnswerStr.pop();
  //   //     }
  //   //   }
  //   //   counter++;
  //   // }

  //    //console.log(">>> " + something);

  //   //console.log(">>>>>> currentAnswerStr: " + this.currentAnswerStr);    
  //   */
  // }
}
</script>

<style>
body{
  background: linen;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  /* background: linen; */
}
.wrongAns{
  background-color:#ffcb0059;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 145px;

  display: grid;
  grid: 30px / auto auto auto auto;
  grid-gap: 3px;
  color: white;
  font-size: 40px;line-height: 25px;letter-spacing: 10px;font-weight: 700;
  margin: 0px auto 5px;
  border: 5px solid lightyellow;
  border-radius: 15px;
}
.wrongAns span{
  opacity: 0.5;
}
.wrongAnsOne{
  color: red;
  opacity: 1 !important;
}
.wrongAnsTwo{
  color: red;
  opacity: 1 !important;
}
.wrongAnsThree{
  color: red;
  opacity: 1 !important;
}
.wrongAnsFour{
  color: red;
  opacity: 1 !important;
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
</style>
