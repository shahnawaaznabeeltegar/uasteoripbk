<template>
  <div class="about-container">
    <div class="about-content">
      <h1 class="about-title">About Us</h1>
      <p class="about-description">
        We are a platform dedicated to connecting users with a variety of interesting and inspirational content. With a focus on unique user experiences, we provide information and entertainment that can inspire your everyday life.
      </p>
      <div class="cta-buttons">
        <router-link to="/features" class="cta-link">Our Features</router-link>
        <router-link to="/contact" class="cta-link">Contact Us</router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();
</script>

<style scoped>
.about-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #1a1a1a; /* Warna latar belakang gelap yang serasi */
  color: #fff;
  text-align: center;
  padding: 20px;
}

.about-content {
  max-width: 600px;
  margin: auto;
}

.about-title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.about-description {
  font-size: 18px;
  line-height: 1.6;
  margin-bottom: 30px;
}

.cta-buttons {
  margin-top: 30px;
}

.cta-link {
  display: inline-block;
  padding: 12px 24px;
  background-color: #007bff;
  color: #fff;
  text-decoration: none;
  border-radius: 5px;
  margin-right: 20px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.cta-link:hover {
  background-color: #0056b3;
}
</style>
