<script setup></script>

<template>
  <section class="slider">
    <div class="container">
      <div class="text-content">
        <h1>¡Quien Soy!</h1>
        <h4>
          Soy un artista digital que fusiona lo psicodélico con el surrealismo,
          creando mundos donde los ojos son testigos de realidades ocultas. Me
          inspiran la naturaleza, los animales y los conceptos abstractos,
          buscando que cada obra revele algo nuevo con cada mirada. Desde
          pequeño, el arte ha sido mi lenguaje; llenaba de dibujos la parte de
          atrás de mis cuadernos mientras mi familia, siempre envuelta en la
          creatividad, sembraba en mí esta pasión. Hoy, a través de la
          ilustración digital, sigo explorando lo desconocido y compartiendo mi
          visión en redes y exposiciones, donde invito a otros a perderse y
          encontrarse en mis creaciones.
        </h4>
      </div>
      <div class="image-content">
        <img src="/images/manzana.png" alt="Imagen representativa" />
      </div>
    </div>

    <div class="container">
      <div class="text-content">
        <h1 class="tx-ve">¡Mi Arte!</h1>
        <h4>
          Mi arte es un viaje psicodélico donde los ojos representan la
          expansión de la percepción, ver más allá de lo evidente y abrir el
          tercer ojo. Creo mundos caóticos, llenos de vida y profundamente
          abstractos, donde cada detalle es una pieza de algo más grande. Uso
          colores vibrantes y composiciones complejas para que cada obra sea una
          experiencia que sorprenda una y otra vez. No quiero que mi arte sea
          solo algo que se mira, sino algo que te atrape, que te haga descubrir
          nuevos elementos cada vez que vuelves a verlo.
        </h4>
      </div>
      <div class="image-content">
        <img src="/images/galery.png" alt="Imagen representativa" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr; /* Dos columnas iguales */
  grid-template-rows: 100vh;
  gap: 40px;
  align-items: center;
  justify-items: center;
  justify-content: center;
  align-content: center;
  padding: 40px;
  background-color: black; /* Color de fondo similar al de la imagen */
  color: white; /* Texto en blanco para contraste */
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.image-content {
  height: 80vh;
}

img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
}

.text-content {
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.container h1 {
  font-family: "Abril Fatface", serif;
  font-style: normal;
  color: rgb(255, 89, 0);
  font-size: 36px;
}

.tx-ve {
  color: rgb(30, 255, 0) !important;
}

.container h4 {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
  text-align: justify;
}
</style>
