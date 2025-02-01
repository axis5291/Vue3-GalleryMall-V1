<template >
    <div class="container">
      <h1>상영 영화</h1>
    <!-- **App.vue의 <Movies :movieListApp="copyMovieList">를 movieListApp로 넘겨받아 영화자료를 출력한다.-->
      <div v-for="(movie) in movieListApp" :key="movie.id" class="item">  <!-- v-for는 :key=""를 지정해줘야 한다 -->
        <figure>
          <img :src="`${movie.url}`" :alt="movie.title" width="200">
          <!-- html 태그 속성에 동적자료를 연결할려면 :('v-bind:')를 사용한다. -->
           <!-- `${}` :백틱 문법이라고 하는데 ``안에 문자와 변수를 같이 작성하는것이 가능하다. -->
        </figure>
    
        <div class="info">
          <h3 class="bg-color" :style="movie.fontColor">제목:{{ movie.title }}</h3>
          <p>연도:{{ movie.year }}</p>
          <p>장르:{{ movie.category }}</p> 
          <button @click="$emit('increaseLikeMovies', movie.id)">좋아요</button>   <!--increaseLikeMovies라는 이름으로 상위로 보냄-->
          <span>{{ movie.count }}</span>
          <p>
            <button @click="$emit('openModal', movie.id)">상세보기</button>
               <!-- 부모컴포넌트에게 1.상세보기를 열게끔하는 이벤트$emit('openModal')와 
                                2.어떤영화를 보여줄지 id-> $emit('openModal', id) 이렇게 2개의 이벤트를 전달해야 한다.
                                 $emit()은 2번째 인자를 값으로 전달할 수 있다 -->
            <!-- v-for에서 정의한 id를 가져와서 사용 -->
            <!-- *이벤트가 값을 2가지 이상을 전달할 때 어떻게 하는지 주목 -->
          </p>
        </div>
       </div> 
    
      </div>
    </template>
    <script>
    export default {
      name:"ImageModalComponent",
    
      props:{    
           //App.vue의 <Modal>태그에서 넘겨준 것을 '변수명:데이터 타입'으로 등록. 
            //그러면 App.vue에서 정의한 변수들을 인식하고 이 파일에서 <template>에서 쓸수 있다. 
         isModalApp:Boolean,
         movieListApp:Array,
         selectedMovieApp:Number,
         increaseLikeApp:Function,
      
      },
    }
    </script>
    
    <style >
      .container{
        padding:20px;
      }
    </style>