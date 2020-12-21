<template>
  <div id="slot">
    <div class="slot-num">
      <!-- スロットを回す速度や配列変数を入れる -->
      <Num @end="end" ref="num_start1" :speed="2000" :array="turtles" ></Num>
      <Num @end="end" ref="num_start2" :speed="1000" :array="turtles" ></Num>
      <Num @end="end" ref="num_start3" :speed="2000" :array="turtles" ></Num>
    </div>
    <!-- ↓ボタン押下で子のstartメソッドが起動 -->
    <button class="start_btn" v-on:click="start" v-if="!slotOn">S t a r t</button>
    <button class="start_btn" v-on:click="start" v-if="slotOn" disabled>S t a r t</button>
    <p v-if="hit===true">当たり！</p>
    <p v-else-if="hit===false && slotEnd===3">残念</p>
    <!-- <p>{{result}}</p> -->
  </div>
</template>



<script>
import Num from './Num.vue'
import turtles from '../assets/turtle.json'
export default {
  name: 'game',
  components:{
    Num
  },
  data() {
    return {
      turtles:turtles,
      info:[
      ],
      slotOn:false,
      slotEnd:0, //Numのスロットのstop()が起動したときに1追加。3になった時、slotOnをfalseにし、0にリセット
      result:[],
      hit:false,
    }
  },
  methods: {
    // スタートボタンを押したとき3つのNumのstart()が起動
    start(){
      this.hit=false;
      this.slotEnd=0;
      this.result=[];
      // 子コンポーネントnumのstartメソッド
      this.$refs.num_start1.start();
      this.$refs.num_start2.start();
      this.$refs.num_start3.start();
      this.slotOn=true;
    },

    complete: function() {
      clearInterval(this.timerObj)
    },
    //Numのstop()起動後、slotEndが1増加
    end(hogi){

      this.slotEnd++;

      // 配列が空||同じ値がある→hairetuに挿入
      if(this.result.length===0 || this.result.includes(hogi)){

        this.result.push(hogi);

      }
      if(this.slotEnd==3){

        //配列の要素数が３（値が揃っている）→当たり
        if(this.result.length===3){

          this.hit=true;
          //揃った画像パスを親のAppに送る
          this.$emit("turtle",hogi);
          
        }
        this.slotOn=false;
        
      }
    },
  },
  computed: {
    
  }
}
</script>



<style scoped>
#slot {
  margin-top:100px;
  text-align: center;
}
.slot-num{
  margin:0 auto;
  display: flex;
  align-items: center;
  justify-content: space-around;
  width:800px;
}
.start_btn{
  margin-top:50px;
  font-size:1.2rem;
}
</style>