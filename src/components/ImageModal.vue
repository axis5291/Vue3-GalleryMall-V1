<template>
  <div v-if="openImageModal" class="modal"  :style="modalStyle" >
    <div class="modal-content" :style="modalContentStyle" @click.stop>
      <img :src="item1.imgPath" @click="$emit('closeModal')"  :alt="item1.name" @load="handleImageLoad" style="cursor: pointer;"/>
    </div>
  </div>
</template>


<script>
import { ref, computed } from "vue";

export default {
  props: {
    openImageModal: Boolean,  
    item1: Object,         //Card.vue에서 <ImageModal :item1="item1">로 받아온 값
  },

setup() {
    const imgWidth = ref(0);
    const imgHeight = ref(0);

    // 이미지 크기를 감지하는 함수
    const handleImageLoad = (event) => {
      imgWidth.value = event.target.naturalWidth;
      imgHeight.value = event.target.naturalHeight;
    };

    // 배경 색상 변경 (가로 vs 세로)
    const modalStyle = computed(() => ({
      background: imgWidth.value > imgHeight.value ? "rgba(0, 0, 0, 0.8)" : "rgba(255, 255, 255, 0.9)",
    }));

    // 모달 크기를 이미지 크기에 맞게 조절
    const modalContentStyle = computed(() => {
      const maxWidth = window.innerWidth * 0.9; // 최대 가로 크기 (화면의 90%)
      const maxHeight = window.innerHeight * 0.9; // 최대 세로 크기 (화면의 90%)

      let width = imgWidth.value;
      let height = imgHeight.value;

      // 크기가 너무 크면 비율 유지하면서 축소
      if (width > maxWidth) {
        const scale = maxWidth / width;
        width *= scale;
        height *= scale;
      }
      if (height > maxHeight) {
        const scale = maxHeight / height;
        width *= scale;
        height *= scale;
      }

      return {
        width: `${width}px`,
        height: `${height}px`,
      };
    });

    return { handleImageLoad, modalStyle, modalContentStyle };
  },
};

</script>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7); /* 반투명 배경 */
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  max-width: 80%; /* 최대 너비 */
  max-height: 80%; /* 최대 높이 */
  overflow: hidden; /* 내부 요소가 넘치지 않도록 */
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal img {
  width: 100%;
  height: auto;
  max-height: 70vh; /* 화면 높이에 맞춰 조절 */
  object-fit: contain; /* 이미지가 잘리지 않도록 */
  border-radius: 5px;
}

/* 모바일 화면 최적화 */
@media (max-width: 768px) {
  .modal-content {
    max-width: 90%;
    max-height: 90%;
  }
  .modal img {
    max-height: 60vh;
  }
}
</style>
