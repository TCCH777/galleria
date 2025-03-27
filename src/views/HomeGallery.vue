<script setup>
import { ref, computed } from "vue";

const props = defineProps({ images: Array });
const itemsPerPage = 3;
const currentIndex = ref(0);
const selectedImage = ref(null);

// Obtener las imágenes visibles actualmente
const visibleImages = computed(() => {
  return props.images.slice(0, currentIndex.value + itemsPerPage);
});

// Cargar más imágenes cuando se hace scroll
const loadMore = () => {
  if (currentIndex.value + itemsPerPage < props.images.length) {
    currentIndex.value += itemsPerPage;
  }
};

// Seleccionar una imagen para ver detalles
const selectImage = (image) => {
  selectedImage.value = image;
};

// Volver a la galería
const backToGallery = () => {
  selectedImage.value = null;
};
</script>

<template>
  <div class="gallery-container">
    <div v-if="!selectedImage" class="gallery">
      <h2>Gallery</h2>
      <div class="images">
        <div
          v-for="image in visibleImages"
          :key="image.Titulo"
          @click="selectImage(image)"
        >
          <img :src="image.ImagenP" :alt="image.Titulo" />
        </div>
      </div>
      <button
        v-if="currentIndex + itemsPerPage < images.length"
        @click="loadMore"
      >
        Cargar más
      </button>
    </div>

    <div v-else class="details">
      <button @click="backToGallery">Volver</button>
      <img :src="selectedImage.ImagenG" :alt="selectedImage.Titulo" />
      <h2>{{ selectedImage.Titulo }}</h2>
      <p>{{ selectedImage.Descripcion }}</p>
      <p><strong>Fecha:</strong> {{ selectedImage.Fecha }}</p>
    </div>
  </div>
</template>

<style scoped>
.gallery-container {
  text-align: center;
  color: #fff;
  background: #111;
  padding: 20px;
}

.gallery .images {
  display: flex;
  gap: 20px;
  overflow-x: auto;
}

.gallery img {
  width: 150px;
  cursor: pointer;
  border-radius: 5px;
}

.details {
  text-align: left;
  padding: 20px;
}

.details img {
  width: 100%;
  max-width: 400px;
  display: block;
  margin-bottom: 10px;
}
</style>
