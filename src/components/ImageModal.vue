<template>
    <!-- 아래는 Modal창 정의,  isModalApp가 true일때 Modal창이 실행된다.-->
    <div class="modal" v-if="openModalApp">         
   
      <div class="inner" @click="$emit('closeModal')">     <!-- 모달창 아무곳이나 클릭하면 닫힘 -->
        <h3>  {{movieListApp[selectedMovieApp].title}}  </h3>
        <!-- <button  selectedMovie=index" >상세보기버튼에서 
             입력된 index값의 selectedMovie를 가져와서 제목을 보여준다 -->
  
        <p>영화 상세정보:{{movieListApp[selectedMovieApp].detailInfo}}</p>
  
        <button @click="$emit('closeModal')">닫기</button>
         <!-- 자식 컴포넌트(Modal.vue)에서 부모 컴포넌트에게 데이터 변경을 요청할 수 있는 방법이
               $emit(임의의 이밴트명) -> App.vue의 <Modal /> 태그로 받는다  
         -->
  
        <!-- Modal컴포넌트로 분리전 원 소스--------
         <button @click="isModal=false">닫기</button>
             isModal이 App.vue에 있기 때문에 이 변수를 전달 받는다. -->
      </div>
     </div>
  </template> 
  
  <script>
     export default{
       name:"ImageModalComponent", //컴포넌트 용도로 쓸려면 명명규칙에 따라 Modal한 다음에 Component를 붙여준다. 
       
       props:{    
         //App.vue의 <Modal>태그에서 넘겨준 것을 '변수명:데이터 타입'으로 등록. 
         //그러면 App.vue에서 정의한 변수들을 인식하고 이 파일에서 <template>에서 쓸수 있다. 
       openModalApp:Boolean,
       movieListApp:Array,
       selectedMovieApp:Number,
       
      },
  
     }
  
    
  </script>
  
  <style>
  
  
  </style>
  
  
  