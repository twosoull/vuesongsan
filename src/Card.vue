    <template>  

    <div v-for="(원룸,i) in 원룸들" :key="i">
        <img class="room-img" :src="원룸.image">
        <h4 @click="모달창열렸니 = true; 누른거 = i">{{ 원룸.title }}</h4>
        <p> {{ 원룸.price }}원</p>
    </div>

      
    </template>
      
    <script>
    export default {
        name : "Card",
        props : {
            원룸들 : Array,
            모달창열렸니 : Boolean,
        }
    }
    </script>
      
    <style>
    
    </style>
      