<template>
  <div id="InputPanel" class="InputPanel">
    <nav v-for="(letter, index) in letters" :key="index" class="inputpanel-nav">
      <a href="#" @click.prevent="$emit('selectLetter', index)" :class="{selected: !letter.active}">
        {{ letter.letter }}
      </a>
    </nav> 
    
    <!--<br>
    <nav v-for="(n, index) in 13" :key="index" class="inputpanel-nav">
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
    
  },
  data(){
    return{

    }
  }
}
</script>

<style scoped>
.InputPanel{
  display:inline-block;
  /*margin:60px auto 45px;*/
  background-color:#5597b4;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  width: 400px;
}
.inputpanel-nav{
    display:inline-block;
    /*margin:60px auto 45px;*/
    background-color:#5597b4;
    padding: 10px;
}
nav a{
    display:inline-block;
    /*padding: 18px 30px;*/
    color:#fff;
    font-weight:bold;
    font-size:16px;
    text-decoration:none;
    line-height:1;
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
  color:grey;
  cursor: default;
}
</style>
