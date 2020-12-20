<template>
   <div class="block">
      <div class="image">
        <img class="slot_img" :src="type.url" alt="" />
      </div>
      <!-- 押すとstartメソッドが起動 -->
      <button class="stop_btn"  v-on:click="stop" v-if="c_slotOn">Stop</button>
      <button class="stop_btn" v-on:click="stop" v-if="!c_slotOn" disabled>Stop</button>
      <p>{{type}}</p>
    </div>
</template>

<script>
export default {
  props:{
    speed:{
      type:Number,
      default:100
      },
      array:{
        default:0
      },
  },
   data() {
    return {
      // array:[0,1,2,3,4,5,6,7],
      type:"?",
      min: 59,
      c: 0, //配列のループさせるindex値
      c_slotOn: false,
      timerObj: null,
      hogi:"",
    }
  },
  methods: {
    count: function() {
      
        this.c++;
        if(this.c>=this.array.length){
          this.c=0;
        }
        this.type=this.array[this.c];
      
    },

    start: function() {
      let self = this;
      this.timerObj = setInterval(function() {self.count()}, this.speed)
      this.c_slotOn = true; 
    },

    stop: function() {
      clearInterval(this.timerObj);
      this.c_slotOn = false; //timerがOFFであることを状態として保持
      this.hogi=this.type;  //hogi...画像パス
      this.c=0;
      this.$emit("end",this.hogi);
    },

    complete: function() {
      clearInterval(this.timerObj)
    }
  },
}
</script>

<style  scoped>
.block{
  width:33.3%;
}
button{
  padding:0 5px;
  font-size:1.2rem;
}
img{
  width:250px;
  height:250px;
  margin:0 auto;
  object-fit: cover;
}
.stop_btn{
  margin-top:10px;
}


</style>