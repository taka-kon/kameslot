<template>
<div>
  <div class="popup" id="js-popup" :class="{'is-show':isShow}">
    <div class="popup-inner">
      <div class="close-btn" id="js-close-btn" @click="closePopUp" >
        <i class="fas fa-times"></i>
      </div>
        <img :src="showTurtle" alt="ポップアップ画像">
        <h2>二ホンイシガメ</h2>
        <p>{{}}</p>
      
    </div>
    <div class="black-background" id="js-black-bg"  @click="closePopUp"></div>
  </div>
    <p>{{showModal()}}</p>
    <!-- showTurtleに.urlや.nameを付けるとモーダルが消えなくなる
    Avoid mutating a prop directly since the value will be overwritten whenever the parent component re-renders. Instead, use a data or computed property based on the prop's value. Prop being mutated: "showTurtle"
     -->

  <!-- <button id="js-show-popup" @click="popImage">Show Popup</button> -->
</div>
</template>

<script>
export default {
  name: 'modal',
  props:{
    name:String,
  },
  data(){
    return{
      show:false, //trueのときモーダル表示
      isShow:false,  //trueのときHTML側で設定されたクラス名is-showが付与
    }
  },
  methods:{
    showModal(){
      if(this.showTurtle!=null){
        this.popImage(this.showTurtle);
      }
    },
    popImage(){
      this.isShow=true;

    },
    closePopUp(){
      this.isShow=false;
      this.showTurtle=null;
    }
  }
 
  
}
</script>

<style scoped>
.popup {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  opacity: 0;
  visibility: hidden;
  transition: .6s;
}
.popup.is-show {
  opacity: 1;
  visibility: visible;
}
.popup-inner {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  width: 80%;
  max-width: 600px;
  padding: 50px;
  background-color: #fff;
  z-index: 2;
}
.popup-inner img {
  width: 100%;
}
.close-btn {
  position: absolute;
  right: 0;
  top: 0;
  width: 50px;
  height: 50px;
  line-height: 50px;
  text-align: center;
  cursor: pointer;
}
.close-btn i {
  font-size: 20px;
  color: #333;
}
.black-background {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,.8);
  z-index: 1;
  cursor: pointer;
}
</style>
