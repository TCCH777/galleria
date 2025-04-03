<template>
  <div class="video-container">
    <video autoplay loop muted playsinline class="background-video">
      <source
        src="https://firebasestorage.googleapis.com/v0/b/portafolio-4ec64.firebasestorage.app/o/yowiiii.mp4?alt=media&token=e10c227f-3c17-439f-aca7-b141fe78ef69"
        type="video/mp4"
      />
    </video>
  </div>

  <div v-if="showGallery" class="gallery-container">
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

const showGallery = ref(false);
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
.video-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  padding: 25px;
}
.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
}

.gallery-container {
  text-align: center;
  background-color: #222;
  color: #90ee90;
  padding: 20px;
}
.gallery-title {
  font-size: 2rem;
  margin-bottom: 20px;
}
.image-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  overflow-y: auto;
  max-height: 500px;
  padding: 10px;
}
.image-wrapper {
  background: #333;
  padding: 20px;
  border-radius: 15px;
  cursor: pointer;
  transition: transform 0.3s;
}
.image-wrapper:hover {
  transform: scale(1.1);
}
.image {
  width: 100%;
  height: auto;
  border-radius: 15px;
}
.detail-view {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.9);
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
</style>
