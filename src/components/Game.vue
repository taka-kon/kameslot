<template>
  <div id="slot">
    <div class="slot-num">
      <!-- スロットを回す速度や配列変数を入れる -->
      <Num @end="end" ref="num_start1" :speed="800" :array="array.a" ></Num>
      <Num @end="end" ref="num_start2" :speed="800" :array="array.b" ></Num>
      <Num @end="end" ref="num_start3" :speed="800" :array="array.c" ></Num>
    </div>
    <!-- ↓ボタン押下で子のstartメソッドが起動 -->
    <button class="start_btn" v-on:click="start" v-if="!slotOn">S t a r t</button>
    <button class="start_btn" v-on:click="start" v-if="slotOn" disabled>S t a r t</button>
    <p v-if="hit===true">当たり！</p>
    <p v-else-if="hit===false && slotEnd===3">残念</p>
  </div>
</template>



<script>
import Num from './Num.vue'
export default {
  name: 'game',
  components:{
    Num
  },
  data() {
    return {
      img:[
        "/img/kusagame.jpg","/img/ishigame.jpg","/img/midorigame.jpg","/img/suppon.jpg","/img/minami.jpg","/img/kiboshi.jpg","/img/umigame.jpg","/img/semaru.jpg","/img/kabuto.jpg","/img/supomodo.jpg"
      ],
      array:{
        a:["/img/kusagame.jpg","/img/ishigame.jpg","/img/midorigame.jpg","/img/suppon.jpg","/img/minami.jpg","/img/kiboshi.jpg","/img/umigame.jpg","/img/semaru.jpg","/img/kabuto.jpg","/img/supomodo.jpg"],
        b:["/img/kusagame.jpg","/img/ishigame.jpg","/img/midorigame.jpg","/img/suppon.jpg","/img/minami.jpg","/img/kiboshi.jpg","/img/umigame.jpg","/img/semaru.jpg","/img/kabuto.jpg","/img/supomodo.jpg"],
        c:["/img/kusagame.jpg","/img/ishigame.jpg","/img/midorigame.jpg","/img/suppon.jpg","/img/minami.jpg","/img/kiboshi.jpg","/img/umigame.jpg","/img/semaru.jpg","/img/kabuto.jpg","/img/supomodo.jpg"]
      },
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
          // window.open( 'https://www.google.com/search?q=%E3%82%AB%E3%83%94%E3%83%90%E3%83%A9&oq=%E3%82%AB%E3%83%94%E3%83%90%E3%83%A9&aqs=chrome..69i57j69i59j35i39j0i395i433j0i131i395i433j69i60l2j69i61.13008j1j7&sourceid=chrome&ie=UTF-8' );
          
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