<template>
  <div class="container">
    <h1 class="slide-in">TUGAS 3</h1>
    <h5 class="slide-in1">Naufal Rizqullah</h5>
    <h5 class="slide-in2">223510805</h5>
    <header></header>

      <!-- Form untuk menambahkan Todo -->
      <div class="input-container">
        <form @submit.prevent="addTodo">
          <input v-model="newTodo" placeholder="Masukkan Kegiatan" class="input-field">
          <button @click="addTodo" class="add-button">Add</button>
        </form>
      </div>

    <!-- Daftar Todo -->
    <div>
      <h3>List Kegiatan</h3>
      <ul class="todo-list">
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          {{ todo.text }}
          <button @click="editTodo(index)" class="edit-button">Edit</button>
          <button @click="deleteTodo(index)" class="delete-button">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '', // Menyimpan nilai input baru
      todos: [],   // Menyimpan daftar todo
    };
  },

  // Memuat daftar todo dari local storage saat komponen dibuat
  created() {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      this.todos = JSON.parse(savedTodos);
    }
  },

  methods: {
    // Menambahkan todo baru
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo });
        this.saveTodos(); // Menyimpan daftar todo setelah ditambahkan
        this.newTodo = ''; // Mengosongkan input setelah ditambahkan
      }
    },

    // Mengedit todo
    editTodo(index) {
      const newText = prompt('Edit Kegiatan', this.todos[index].text);
      if (newText !== null) {
        this.todos[index].text = newText;
        this.saveTodos(); // Menyimpan daftar todo setelah diedit
      }
    },

    // Menghapus todo
    deleteTodo(index) {
      if (confirm('Apakah Kamu Yakin Untuk Menghapus Kegiatan Ini?')) {
        this.todos.splice(index, 1);
        this.saveTodos(); // Menyimpan daftar todo setelah dihapus
      }
    },

    // Menyimpan daftar todo ke local storage
    saveTodos() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
  border: 5px solid gray;
  border-radius: 20px;
  padding: 20px;
  background-image: url('https://r4.wallpaperflare.com/wallpaper/684/971/825/studio-ghibli-anime-cartoon-japanese-my-neighbor-totoro-hd-wallpaper-9886add810b0bcd8a06ce13e78a2547a.jpg');
  background-size: cover;
  background-position: center;
  background-color: rgba(255, 255, 255, 10); 
}

.container h1 {
  margin-top: 10px; 
}

.container h5 {
  margin-top: 10px; 
  text-align: left;
}
h1{
  font-size: 35px;
}
header {
  border-bottom: 2px dashed silver;
}

.input-container {
  display: flex;
  align-items: center;
  margin-top: 30px;
}

.input-field {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
  font-size: 16px;
}

.add-button {
  padding: 10px 20px;
  background-color: #40679E;
  color: white;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  font-size: 16px;
}

.add-button:hover {
  background-color: #696969;
  color: black;
}

.edit-button {
  padding: 10px 20px;
  background-color: #40679E;
  color: white;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  font-size: 16px;
}

.edit-button:hover {
  background-color: #696969;
  color: black;
}

.delete-button {
  padding: 10px 20px;
  background-color: #40679E;
  color: white;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  font-size: 16px;
}

.delete-button:hover {
  background-color: #696969;
  color: black;
}

.todo-list {
  list-style:none ;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px dashed #ddd;
  border-radius: 5px;
}
</style>