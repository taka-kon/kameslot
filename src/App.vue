<template>
  <div id="app">
    <div class="header">
      カメ合わせ
    </div>
    <Game @turtle="showTurtle"></Game>
  </div>
</template>

<script>
import Game from './components/Game.vue'
export default {
  name: 'app',
  components:{
    Game
  },
  methods:{
    showTurtle(hogi){
      if(hogi==="/img/kusagame.jpg"){
        window.open( 'https://www.youtube.com/watch?v=QuNiIjKutEA' );
      }else if(hogi==="/img/ishigame.jpg"){
        window.open('https://www.youtube.com/watch?v=IBAvGXZ7OvM');
      }else if(hogi==="/img/kabuto.jpg"){
        window.open('https://www.youtube.com/watch?v=2ejdGwdFsB0');
      }
    }
  }
 
  
}
</script>

<style scoped>
@import "./css/Modern.css";
*{
  font-size:62.5%;
}
.header{
  background-color:rgb(255, 228, 228);
  padding:20px;
  text-align: center;
  font-size:2rem;
}
</style>