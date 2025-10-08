<template>
  <div class="app">
    <h1>📝 My Todo List (with Query String)</h1>

    <div class="input-area">
      <input
        v-model="newTask"
        placeholder="הוסף משימה חדשה..."
        @keyup.enter="addTask"
      />
      <button @click="addTask">הוסף</button>
    </div>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task }}
        <button class="delete" @click="removeTask(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask.trim())
        this.newTask = ''
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1)
    },
    checkQueryString() {
      const params = new URLSearchParams(window.location.search)
      const taskFromUrl = params.get('task')
      if (taskFromUrl) {
        this.tasks.push(decodeURIComponent(taskFromUrl))
      }
    }
  },
  mounted() {
    this.checkQueryString()
  }
}
</script>

<style>
.app {
  font-family: Calibri, sans-serif;
  text-align: center;
  max-width: 350px;
  margin: 60px auto;
  background: #f9f9f9;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  margin-bottom: 20px;
}

.input-area {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
}

input {
  padding: 8px;
  width: 70%;
  border: 1px solid #ccc;
  border-radius: 6px;
}

button {
  margin-left: 8px;
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  background-color: black;
  color: white;
  cursor: pointer;
}

button.delete {
  background-color: red;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  background: white;
  border-radius: 6px;
  margin-top: 8px;
  padding: 8px 10px;
}
</style>
