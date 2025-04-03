<template>
  <!-- Contact Section -->
  <div class="contact-section">
    <h2 class="contact-title">Commission Art</h2>
    <form @submit.prevent="sendEmail" class="contact-form">
      <input
        type="text"
        v-model="formData.name"
        placeholder="Your Name"
        required
      />
      <input
        type="email"
        v-model="formData.email"
        placeholder="Your Email"
        required
      />
      <textarea
        v-model="formData.message"
        placeholder="Your Message"
        required
      ></textarea>
      <button type="submit">Send Email</button>
    </form>
    <a :href="whatsappLink" target="_blank" class="whatsapp-button">
      <img src="/images/whatsapp-icon.png" alt="WhatsApp" />
    </a>
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

// Contact Form Logic
const formData = ref({ name: "", email: "", message: "" });
const sendEmail = () => {
  const mailtoLink = `mailto:italocianci00@gmail.com?subject=Art Inquiry&body=Name: ${formData.value.name}%0D%0AEmail: ${formData.value.email}%0D%0AMessage: ${formData.value.message}`;
  window.location.href = mailtoLink;
};

const whatsappLink = "https://wa.me/573215397661";
</script>

<style scoped>
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
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.3s;
}
.image-wrapper:hover {
  transform: scale(1.1);
}
.image {
  width: 100%;
  height: auto;
  border-radius: 10px;
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

/* Contact Section */
.contact-section {
  background: black;
  color: #ff0000;
  text-align: center;
  padding: 40px 20px;
}
.contact-title {
  font-size: 2rem;
  margin-bottom: 20px;
}
.contact-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.contact-form input,
.contact-form textarea {
  width: 80%;
  padding: 10px;
  background: #222;
  border: 1px solid #ff0000;
  color: white;
}
.contact-form button {
  background: #90ee90;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-weight: bold;
}
.whatsapp-button img {
  margin-top: 20px;
  width: 50px;
}
</style>
