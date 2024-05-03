<template>

<transition name="fade">
  <Modal @closeModal="모달창열렸니=false;" 
  :원룸들="원룸들" :모달창열렸니="모달창열렸니" :누른거="누른거"/>
</transition>

  <div class="menu">
    <a v-for="(a,i) in 메뉴들" :key="i" >{{a}}</a>
  </div>

  <Discount v-if="showDiscount" :DiscountValue="DiscountValue"/>
  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <Card @openModal="모달창열렸니 = true; 누른거= $event" v-for="(a,i) in 원룸들" :원룸="원룸들[i]" :key="i"/>

</template>

<script>

import data from './oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';
export default {
  name: 'App',
  data(){
    return {
      DiscountValue : 5,
      showDiscount : true,
      원룸들오리지널 : [...data],
      오브젝트 : {name : 'kim', age : 20},
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      products: ['역삼동원룸','천호동원룸','마포구원룸'],
      메뉴들 : ['Home','Shop', 'About'],
    }
  },
  methods : {
    increase(num){
      this.신고수[num] += 1;
    },
    priceSort(){
      this.원룸들.sort(function(a,b){
        return a.price - b.price
      });
      //[3,5,2].sort(); //2,3,5 이건 문자순 정렬임
      /*[3,5,2].sort(function(a,b){
        return a-b
      })*/ //숫자 순 정렬

    },
    sortBack(){
      //this.원룸들 = this.원룸들오리지널; 
      //array를 = 하면왼쪽 오른쪽은 값을 공유해주세요가 된다.

      this.원룸들 = [...this.원룸들오리지널]; 
    }
  },
  mounted(){


      setInterval(()=>{
        //1초마다 내부 코드가 실행 됌
        this.DiscountValue--;
      },1000)
    
  },
  updated(){
    if(this.DiscountValue < 1){
      this.showDiscount = false;
    }
  },
  components: {
    Discount,
    Modal,
    Card,
  }
}
</script>

<style>
.fade-enter-from{/*시작*/
  transform : translateY(-1000px);
}
.fade-enter-active{ /*transition*/
  transition : all 1s;
}
.fade-enter-to{/*끝*/
  transform : translateY(0px);
}

.fade-leave-from{/*시작*/
  opacity:1;
}
.fade-leave-active{ /*transition*/
  transition : all 1s;
}
.fade-leave-to{/*끝*/
  opacity:0;
}

.start{
  opacity : 0;
  transition: all 1s;
}
.end{
  opacity : 1;
}

body{
  margin : 0
}
div{
  box-sizing: border-box;
}
.discount{
  background: #eee;
  padding : 10px;
  margin : 10px;
  border-radius: 5px;
}
.black-bg{
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position:fixed; padding : 20px;
}
.white-bg{
  width:100%; background: white;
  border-radius: 8px;
  padding : 20px;
}
.room-img {
  width : 100%;
  margin-top : 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding : 15px;
  border-radius: 5px;
}
.menu a {
  color : white;
  padding : 10px;
}
</style>
