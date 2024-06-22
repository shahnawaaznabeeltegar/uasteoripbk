<template>
  <div>
    <header class="header">
      <nav class="menu">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
          <li><router-link to="/posts">Posts</router-link></li>
          <li><router-link to="/albums">Albums</router-link></li>
          <li><router-link to="/about">About</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<style>
.header {
  background-color: #1a1a2e; /* Ganti warna background */
  padding: 20px;
  text-align: center;
}

.menu ul {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu ul li {
  margin: 0 15px;
}

.menu ul li a {
  text-decoration: none;
  color: #ffffff; /* Ganti warna teks */
  font-weight: bold;
  font-size: 24px; /* Ganti ukuran font */
  padding: 10px 20px;
  border-radius: 10px; /* Ubah border-radius lebih kecil */
  transition: background-color 0.3s, transform 0.2s; /* Ubah durasi animasi */
}

.menu ul li a:hover {
  background-color: #4ecdc4; /* Ganti warna background saat hover */
  transform: scale(1.03); /* Sesuaikan scale transformasi */
}
</style>
