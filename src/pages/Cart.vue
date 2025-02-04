<template>
    <div class="cart">
      <div class="container">
        <ul>
          <li v-for="(item1, index) in state.items" :key="index"  class="d-flex align-items-center">
            <!-- $$  ImageModal.vue로 :item1="item1"을 보냄 -->  
            <ImageModal :openImageModal="openImageModal" :item1="item1" @closeModal="openImageModal=false;" />
            <!-- ImageModal.vue에서 @click="$emit('closeModal')"로 보낸 것을 @closeModal로 받아 openImageModal=false로 설정-->

            <img :src="item1.imgPath" @click="openImageModal = true" class="me-3" style="cursor: pointer;" />
            
            <span class="name">제목:{{ item1.name }}</span>
            <span class="price ms-3"> 할인가:₩{{ lib.getCommaFormated(item1.price -(item1.price*item1.discountPrice/100)) }}</span>
            <i class="fa fa-trash ms-auto text-danger fs-6" style="cursor: pointer;" @click="remove(item1.id)"> 삭제</i>  <!-- 쓰레기통 모양 -->
          </li>
        </ul>
        <router-link to="/order" class="btn btn-primary">구입하기</router-link>
        <!-- 클릭하면 /order로 이동 -->
      </div>
     </div>
</template>

<script>
import axios from 'axios';
import lib from "@/scripts/lib";
import { reactive, ref } from 'vue';
import ImageModal from "../components/ImageModal.vue";

export default{
    name:'CartComponent',
    components:{
      ImageModal:ImageModal
    },
    setup(){
      const openImageModal=ref(false); //$$ 모달창을 열기위한 변수를 선언한다.
      const state=reactive({
          items:[]
      });

      const load=()=>{
        axios.get("/api/cart/items").then((res)=>{
        console.log("cart에서 꺼내보기:", res.data);  //+를 시용하면 객체를 문자열로 변환하여 출력 [object Object]
        state.items=res.data;
       })
      };

      load(); //컴포넌트가 생성될 때 한번만 실행

      const remove=(itemId)=>{
        axios.delete(`/api/cart/items/${itemId}`).then(()=>{
          load();
          console.log(itemId+"번 itemId:"+"장바구니에서 삭제 성공");
        })
      };

      return {state, lib, remove,openImageModal}
    }
} 
</script>

<style scoped>
.cart ul {
  list-style:none;
  margin: 0;
  padding: 0;
}

.cart ul li{
  border:1px solid #eee;
  margin-top: 25px;
  margin-bottom: 25px;
}

.cart ul li img {
  width: 150px;
  height: 150px;
}

.cart ul li .name{
  margin-left: 25px;
}

.cart ul li .price {
  margin-left: 25px;
}

.cart ul li i {
  float: right;
  font-size: 20px;
  margin-right: 50px;
  margin-top: 60;
}

.cart .btn{
  width: 300px;
  display: block;
  margin: 0 auto;
  padding:30px 50px;
  font-size: 20px;
}
</style>







