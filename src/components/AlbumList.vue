<template>
  <div class="albums-container">
    <h2 class="albums-title">Albums</h2>
    <div v-if="albums.length">
      <div class="albums-list">
        <div v-for="album in albums" :key="album.id" @click="viewAlbum(album.id)" class="album-item">
          <div class="album-item-content">
            <div class="album-thumbnail">
              <img :src="getAlbumThumbnail(album.id)" alt="Album Thumbnail">
            </div>
            <div class="album-details">
              <div class="album-id">ID: {{ album.id }}</div>
              <div class="album-title">{{ album.title }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="no-albums">
      <p>No albums available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useAlbumsStore } from '../stores/albums'
import { useRouter } from 'vue-router'

const albumsStore = useAlbumsStore()
const albums = ref([])
const router = useRouter()

const fetchAlbums = async () => {
  await albumsStore.fetchAlbums()
  albums.value = albumsStore.albums
}

const viewAlbum = (id) => {
  router.push(`/albums/${id}`)
}

onMounted(fetchAlbums)

const getAlbumThumbnail = (albumId) => {
  // Placeholder URL or logic to get album thumbnail
  return `https://via.placeholder.com/150?text=Album${albumId}`
}
</script>

<style scoped>
.albums-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.albums-title {
  color: #007bff;
  font-weight: bold;
  margin-bottom: 20px;
}

.albums-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.album-item {
  cursor: pointer;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.album-item:hover {
  transform: translateY(-5px);
  background-color: #007bff;
  color: white;
}

.album-item-content {
  display: flex;
  align-items: center;
}

.album-thumbnail {
  flex: 0 0 100px;
  height: 100px;
  overflow: hidden;
  border-radius: 8px 0 0 8px;
}

.album-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.album-details {
  flex: 1;
  padding: 15px;
  text-align: left;
}

.album-id {
  font-weight: bold;
  margin-bottom: 5px;
}

.album-title {
  font-size: 16px;
  font-family: 'Arial', sans-serif;
}
  
.no-albums {
  text-align: center;
  margin-top: 20px;
}

.no-albums p {
  color: #888;
}
</style>
