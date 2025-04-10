<template>
  <div class="gallery-container">
    <h1 class="gallery-title">Gallery</h1>
    <div class="image-grid" @scroll="handleScroll" ref="scrollContainer">
      <div
        v-for="(image, index) in displayedImages"
        :key="index"
        class="image-wrapper"
        @click="selectImage(image)"
      >
        <img :src="image.ImagenP" :alt="image.Titulo" class="image" />
      </div>
    </div>
  </div>

  <div v-if="selectedImage" class="detail-view">
    <img :src="selectedImage.ImagenG" class="detail-image" />
    <div class="detail-info">
      <h2>{{ selectedImage.Titulo }}</h2>
      <p>{{ selectedImage.Descripcion }}</p>
      <p><strong>Fecha:</strong> {{ selectedImage.Fecha }}</p>
      <button @click="selectedImage = null">Cerrar</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const props = defineProps({
  images: Array,
});

const selectedImage = ref(null);
const scrollContainer = ref(null);
const itemsPerPage = 6;
const currentPage = ref(1);

const displayedImages = computed(() =>
  props.images.slice(0, currentPage.value * itemsPerPage)
);

const handleScroll = () => {
  if (!scrollContainer.value) return;
  const { scrollTop, scrollHeight, clientHeight } = scrollContainer.value;
  if (scrollTop + clientHeight >= scrollHeight - 20) {
    currentPage.value++;
  }
};

const selectImage = (image) => {
  selectedImage.value = image;
};
</script>

<style scoped>
.gallery-container {
  text-align: center;
  background-color: #222;
  color: #90ee90;
  padding: 40px;
}
.gallery-title {
  font-size: 2rem;
  margin-bottom: 20px;
}
.image-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  align-items: center;
  gap: 30px;
  overflow-y: auto;
  overflow-x: hidden;
  max-height: 600px;
  padding: 10px;
}
.image-wrapper {
  cursor: pointer;
  transition: transform 0.3s;
}
.image-wrapper:hover {
  transform: scale(1.1);
}
.image {
  width: 75%;
  height: auto;
  border-radius: 10px;
}
.detail-view {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgb(0, 0, 0);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  padding: 20px;
}
.detail-image {
  max-width: 40%;
  border-radius: 10px;
}
.detail-info {
  max-width: 50%;
  padding-left: 20px;
}
button {
  margin-top: 10px;
  padding: 10px;
  background: #90ee90;
  border: none;
  cursor: pointer;
}

@media screen and (max-width: 768px) {
  .image-grid {
    display: flex;
    flex-direction: column;
    align-items: center;
    overflow-y: auto;
    max-height: none;
    gap: 20px;
    padding-bottom: 80px; /* espacio para que no quede pegado abajo */
  }

  .image-wrapper {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .image {
    width: 90%;
    height: auto;
    border-radius: 10px;
  }

  .detail-view {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: #000;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px 10px;
    overflow-y: auto;
    z-index: 9999;
    touch-action: manipulation;
  }

  .detail-image {
    width: 100%;
    height: auto;
    border-radius: 10px;
    margin-bottom: 20px;
  }

  .detail-info {
    width: 100%;
    flex: 1;
    overflow-y: auto;
    color: white;
    text-align: center;
    padding: 10px;
    font-size: 14px;
    line-height: 1.5;
  }

  .detail-info h2 {
    margin-bottom: 10px;
    font-size: 1.2rem;
    font-weight: bold;
  }

  .detail-info p {
    margin-bottom: 12px;
  }

  button {
    width: 100%;
    padding: 12px;
    font-size: 16px;
    background: #90ee90;
    border: none;
    border-radius: 5px;
    font-weight: bold;
    cursor: pointer;
    margin-top: 20px;
    touch-action: manipulation;
  }

  button:active {
    background-color: #76d376;
  }
}
</style>
