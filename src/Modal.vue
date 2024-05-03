<template>

<div class="black-bg" v-if="모달창열렸니">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" />
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <input v-model.number = "month"/>
      <p>{{ month }} 개월 선택함 {{ 원룸들[누른거].price * month }} 원</p>
      <button @click="$emit('closeModal')">닫기</button> <!--사용불가-->
      <Discount />
    </div>
  </div>
  
</template>
  
<script>
export default {
    name : 'Modal',
    data(){
      return{
        month : 1,
      }
    },
    beforeUpdate(){
      if(this.month == 2){
        alert('3개월부터 가능')
        this.month = 3;
      }
    },
    watch : {
      month(a,b){
        //a는 month데이터가 된다.(변경 후 데이터)
        //b는 변경 전 데이터
        if(a>=13){
          alert("13 이상 입력하지 마셈");
  
        }

        if(isNaN(a)){
          alert('문자는 다메');
        }
      }
    },
    props :{
        원룸들 : Array,
        모달창열렸니 : Boolean,
        누른거 : Number,
    }
}
</script>
  
<style>

</style>
  