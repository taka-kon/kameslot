<template>
  <div id="app">
    <div class="header">
      <h1>カメスロット</h1>
    </div>
    <Modal :showTurtle="turtle" ></Modal>
    <Game @turtle="sendTurtle"></Game>
    <!-- <p>{{turtle}}</p> -->
  </div>
</template>

<script>
import Game from './components/Game.vue'
import Modal from './components/Modal.vue'
export default {
  name: 'app',
  data(){
    return{
      turtle:null,
    }
  },
  components:{
    Game,
    Modal
  },
  methods:{
    sendTurtle(hogi){
      this.turtle=hogi;
    },
    doNull(){
      
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