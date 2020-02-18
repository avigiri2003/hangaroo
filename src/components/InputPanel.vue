<template>
  <div id="InputPanel" class="InputPanel">
    <nav v-for="(letter, index) in letters" :key="index" 
      class="inputpanel_nav" 
      :class="{inputpanel_nav_selected: !letter.active}">
      <a href="#" @click.prevent="$emit('selectLetter', index)" :class="{selected: !letter.active}">
        {{ letter.letter }}
      </a>
    </nav> 
    
    <!--<br>
    <nav v-for="(n, index) in 13" :key="index" class="inputpanel_nav">
      <a href="#">
        {{ String.fromCharCode(index+78) }}
      </a>
    </nav>-->
  </div>
</template>

<script>

export default {
  name: 'InputPanel',
  props: {
    letters: Array,
    selectLetter: Function
  },
  components: {
  }
}
</script>

<style scoped>

* {
  font-family: Consolas;
}

.InputPanel{
  display:inline-block;
  background-color:#ffcb0059;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 700px;

  display: grid;
  grid: 50px / auto auto auto auto auto auto auto auto auto auto auto auto auto;
  grid-gap: 3px;
  /* background-color: #2196F3; */
  /* background-color: #F39721; */
  padding: 10px;
  /* color: lightgreen; */
  color: white;
  font-size: 50px;line-height: 10px;letter-spacing: 0px;font-weight: 700;
  margin: 10px auto 15px;
  border: 5px solid lightblue;
  border-radius: 25px;
}
.inputpanel_nav{
  display:inline-block;
  text-align: center;
  padding: 20px 0;
  font-size: 40px;
  border-radius: 30%;
  box-shadow: 0 2px 8px rgb(52, 170, 48) inset;
  height: 10px;
  width: 50px;
  background-color: rgb(97, 225, 97);
}


.inputpanel_nav_selected{
  display:inline-block;
  text-align: center;
  padding: 20px 0;
  font-size: 40px;
  border-radius: 15px;
  box-shadow: 0 2px 8px rgb(52, 170, 48) inset;
  height: 10px;
  width: 50px;
  background-color: #fff0a0;
  opacity: 70% !important;
}
nav a{
    display:inline-block;
    /*padding: 18px 30px;*/
    color:#fff;
    font-weight:bold;
    text-decoration:none;
    text-transform: uppercase;
    background-color:transparent;

    -webkit-transition:background-color 0.25s;
    -moz-transition:background-color 0.25s;
    transition:background-color 0.25s;
}

nav a:first-child{
    border-radius:2px 0 0 2px;
}

nav a:last-child{
    border-radius:0 2px 2px 0;
}
.selected{
  pointer-events: none;
  cursor: default;
}
</style>
