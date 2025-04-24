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
  .gallery-container {
    padding: 20px 10px;
    background-color: #222;
    color: #90ee90;
    overflow-y: auto;
    max-height: none;
  }

  .gallery-title {
    font-size: 1.5rem;
    margin-bottom: 15px;
  }

  .image-grid {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    max-height: none;
    overflow: visible;
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
    justify-content: flex-start;
    color: white;
    padding: 20px;
    overflow-y: auto;
  }

  .detail-image {
    width: 90%;
    height: auto;
    max-height: 40vh;
    border-radius: 10px;
    margin-bottom: 15px;
  }

  .detail-info {
    width: 90%;
    max-height: 50vh;
    overflow-y: auto;
    padding: 10px;
    text-align: center;
    font-size: 14px;
    line-height: 1.5;
  }

  .detail-info h2 {
    font-size: 1.2rem;
    margin-bottom: 10px;
  }

  .detail-info p {
    margin-bottom: 10px;
  }

  button {
    margin-top: 15px;
    padding: 10px 20px;
    background: #90ee90;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 14px;
    width: auto;
  }
  .gallery-container {
    padding: 20px 10px;
    background-color: #222;
    color: #90ee90;
    overflow-y: auto;
    max-height: none;
  }

  .gallery-title {
    font-size: 1.5rem;
    margin-bottom: 15px;
  }

  .image-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr); /* Mantener grilla en móviles */
    align-items: center;
    gap: 20px;
    max-height: none;
    overflow-y: auto; /* Asegura el scroll en móvil */
    overflow-x: hidden;
    padding: 10px;
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
    justify-content: flex-start;
    color: white;
    padding: 20px;
    overflow-y: auto;
  }

  .detail-image {
    width: 90%;
    height: auto;
    max-height: 40vh;
    border-radius: 10px;
    margin-bottom: 15px;
  }

  .detail-info {
    width: 90%;
    max-height: 50vh;
    overflow-y: auto;
    padding: 10px;
    text-align: center;
    font-size: 14px;
    line-height: 1.5;
  }

  .detail-info h2 {
    font-size: 1.2rem;
    margin-bottom: 10px;
  }

  .detail-info p {
    margin-bottom: 10px;
  }

  button {
    margin-top: 15px;
    padding: 14px 24px; /* Botones más grandes en móvil */
    background: #90ee90;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    width: 100%; /* Que ocupe el ancho en móvil */
  }

  /* Botón extra opcional para compartir */
  .share-button {
    margin-top: 10px;
    padding: 14px 24px;
    background: #4caf50;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 16px;
    cursor: pointer;
    width: 100%;
  }
  .image-grid {
    max-height: 80vh;
    overflow-y: auto !important;
  }
}
</style>
