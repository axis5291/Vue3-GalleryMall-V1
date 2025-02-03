<template>
  <div class="container">
    <!-- App.vue에서 넘겨준 openModalApp이 true이면 모달창이 열린다. Test 다시 수정정-->
  </div>


</template> 
  
  <script>
     export default{
       name:"ImageModalComponent",  //컴포넌트 용도로 쓸려면 명명규칙에 따라 Modal한 다음에 Component를 붙여준다. 
       
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
  
  
  