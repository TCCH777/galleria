<script setup>
import { ref } from "vue";

const slides = [
  {
    title: "¡Quien Soy!",
    text: "Mi nombre es Italo Cianci Chiriboga y soy un artista digital que fusiona lo psicodélico con el surrealismo, creando mundos donde los ojos son testigos de realidades ocultas. Me inspiran la naturaleza, los animales y los conceptos abstractos, buscando que cada obra revele algo nuevo con cada mirada. Desde pequeño, el arte ha sido mi lenguaje; llenaba de dibujos la parte de atrás de mis cuadernos mientras mi familia, siempre envuelta en la creatividad, sembraba en mí esta pasión. Hoy, a través de la ilustración digital, sigo explorando lo desconocido y compartiendo mi visión en redes y exposiciones, donde invito a otros a perderse y encontrarse en mis creaciones.",
    image: "/images/Yovangouh.jpeg",
    color: "rgb(255, 89, 0)",
  },
  {
    title: "¡Mi Arte!",
    text: "Mi arte es un viaje psicodélico donde los ojos representan la expansión de la percepción, ver más allá de lo evidente y abrir el tercer ojo. Creo mundos caóticos, llenos de vida y profundamente abstractos, donde cada detalle es una pieza de algo más grande. Uso colores vibrantes y composiciones complejas para que cada obra sea una experiencia que sorprenda una y otra vez. No quiero que mi arte sea solo algo que se mira, sino algo que te atrape, que te haga descubrir nuevos elementos cada vez que vuelves a verlo.",
    image: "/images/galery.png",
    color: "rgb(30, 255, 0)",
  },
];

const currentIndex = ref(0);

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % slides.length;
};

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + slides.length) % slides.length;
};
</script>

<template>
  <div class="slider">
    <div
      class="slide"
      :style="{ transform: `translateX(-${currentIndex * 50}%)` }"
    >
      <div v-for="(slide, index) in slides" :key="index" class="container">
        <div class="text-content">
          <h1 :style="{ color: slide.color }">{{ slide.title }}</h1>
          <h4>{{ slide.text }}</h4>
        </div>
        <div class="image-content">
          <img :src="slide.image" alt="Imagen representativa" />
        </div>
      </div>
    </div>
    <button class="arrow left" @click="prevSlide">&#9664;</button>
    <button class="arrow right" @click="nextSlide">&#9654;</button>
  </div>
</template>

<style scoped>
.slider {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: start;
}

.slide {
  display: flex;
  width: 200vw;
  transition: transform 0.5s ease-in-out;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 100vw;
  align-items: center;
  padding: 40px;
  color: white;
}

.image-content {
  height: 80vh;
}

img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.text-content {
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

h1 {
  font-family: "Abril Fatface", serif;
  font-size: 36px;
}

h4 {
  font-family: "Montserrat", sans-serif;
  text-align: justify;
}

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: rgb(255, 102, 0);
  font-size: 2rem;
  cursor: pointer;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.arrow:hover {
  opacity: 1;
}

.left {
  left: 10px;
}

.right {
  right: 10px;
}

@media screen and (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto;
    text-align: center;
    padding: 20px;
  }

  .text-content {
    align-items: center;
    text-align: center;
  }

  h1 {
    font-size: 28px;
  }

  h4 {
    font-size: 14px;
  }

  .image-content {
    height: 50vh;
    margin-top: 20px;
  }

  img {
    object-fit: contain;
  }

  .arrow {
    font-size: 1.5rem;
  }
}
</style>
