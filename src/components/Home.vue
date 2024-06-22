<template>
  <div class="home-container">
    <div class="home-content">
      <h1 class="home-title">Welcome to Our Website!</h1>
      <p class="home-description">Explore the Digital World With Us. Discover Various Interesting Stories, Stunning Photo Galleries, and More!</p>
      <router-link to="/about" class="btn" @click="handleAboutClick">About Us</router-link>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    handleAboutClick() {
      this.$router.push('/about');
    }
  }
}
</script>

<style>
.home-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-image: linear-gradient(to right bottom, rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)), url('https://example.com/new-background-image.jpg');
  background-size: cover;
  background-position: center;
  background-blend-mode: overlay; /* Efek gelap untuk latar belakang */
  color: #fff;
  text-align: center;
  padding: 20px;
}

.home-content {
  max-width: 600px;
  margin: 0 auto;
}

.home-title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8); /* Bayangan teks lebih tebal */
}

.home-description {
  font-size: 24px;
  margin-bottom: 30px;
}

.btn {
  display: inline-block;
  padding: 15px 30px;
  background-color: #ff6600; /* Warna tombol yang lebih mencolok */
  color: #fff;
  text-decoration: none;
  border-radius: 30px;
  font-size: 18px;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #cc5500; /* Warna saat tombol dihover */
}
</style>
