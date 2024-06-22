<template>
  <div class="body">
    <section class="create-todo">
      <h2>Apa Rencanamu Hari Ini?</h2>
      <form @submit.prevent="addTodo">
        <label>Masukkan Kegiatan:</label>
        <input type="text" placeholder="Masukkan kegiatanmu" v-model="inputContent" />
        <label>Pilih Kategori:</label>
        <div class="options">
          <label>
            <input type="radio" name="category" value="home" v-model="inputCategory" />
            <span class="bubble home"></span>
            Rumah
          </label>
          <label>
            <input type="radio" name="category" value="assignment" v-model="inputCategory" />
            <span class="bubble task"></span>
            Tugas
          </label>
          <label>
            <input type="radio" name="category" value="work" v-model="inputCategory" />
            <span class="bubble work"></span>
            Kerja
          </label>
        </div>
        <button type="submit">Tambah</button>
      </form>
    </section>

    <section class="todo-list">
      <table>
        <thead>
          <tr>
            <th>Kegiatan</th>
            <th>Kategori</th>
            <th>Aksi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="todo in todosAsc" :key="todo.createdAt" :class="`todo-item ${todo.done ? 'done' : ''}`">
            <td>{{ todo.content }}</td>
            <td>{{ todo.category }}</td>
            <td>
              <button class="delete" @click="removeTodo(todo)">Hapus</button>
            </td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from 'vue'

const todos = ref([])
const inputContent = ref('')
const inputCategory = ref(null)

const todosAsc = computed(() => todos.value.slice().sort((a, b) => b.createdAt - a.createdAt))

const addTodo = () => {
  if (inputContent.value.trim() === '' || inputCategory.value === null) {
    return
  }

  todos.value.push({
    content: inputContent.value,
    category: inputCategory.value,
    done: false,
    createdAt: new Date().getTime()
  })

  inputContent.value = ''
  inputCategory.value = null
}

const removeTodo = todo => {
  todos.value = todos.value.filter(t => t !== todo)
}

watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true })

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
</script>

<style>
.body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #1a1a1a; /* Warna latar belakang utama */
  font-family: 'Arial', sans-serif;
  color: #fff;
}

.create-todo, .todo-list {
  width: 100%;
  max-width: 800px;
  margin: 20px;
  padding: 30px;
  background-color: rgba(0, 0, 0, 0.8); /* Warna latar belakang untuk bagian form dan todo-list */
  border-radius: 10px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.6);
}

.create-todo h2 {
  font-size: 36px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
  color: #000; /* Warna teks judul h2 */
}

.create-todo form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.create-todo label {
  font-size: 18px;
  margin-bottom: 10px;
  color: #007bff; /* Warna teks label */
}

.create-todo input[type="text"] {
  padding: 12px;
  width: 100%;
  margin-bottom: 15px;
  border: 1px solid #666;
  border-radius: 5px;
  font-size: 16px;
  color: #007bff; /* Warna teks input */
}

.create-todo .options {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
}

.create-todo .options label {
  display: flex;
  align-items: center;
  cursor: pointer;
  margin: 0 15px;
  color: #007bff; /* Warna teks label opsi */
}

.create-todo .options .bubble {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  margin-right: 10px;
  border: 2px solid transparent;
  transition: all 0.3s;
  background-color: #007bff; /* Warna latar belakang bubble */
}

.create-todo .options input[type="radio"] {
  display: none;
}

.create-todo .options input[type="radio"]:checked + .bubble {
  border-color: #007bff;
}

.create-todo button[type="submit"] {
  padding: 12px 24px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
  font-size: 16px;
}

.create-todo button[type="submit"]:hover {
  background-color: #0056b3;
}

.todo-list table {
  width: 100%;
  border-collapse: collapse;
  background-color: rgba(255, 255, 255, 0.9);
  margin-top: 30px;
}

.todo-list th, .todo-list td {
  padding: 14px;
  text-align: center;
  border-bottom: 1px solid #ddd;
  color: #000; /* Warna teks pada tabel */
}

.todo-list th {
  background-color: #333;
  color: #fff;
}

.todo-list tr:hover {
  background-color: #f0f0f0;
}

.todo-list .todo-item.done {
  background-color: #f0f0f0;
}

.todo-list .todo-item .delete {
  background: none;
  color: #dc3545;
  border: none;
  cursor: pointer;
  transition: color 0.3s;
}

.todo-list .todo-item .delete:hover {
  color: #c82333;
}
</style>
