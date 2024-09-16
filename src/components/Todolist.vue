<script setup>
import { ref } from 'vue'
import IconTodo from "@/components/icons/IconTodo.vue";

const header = ref('My ToDo-list')
const items = ref([
  { id: 1, label: "Frukost", isGreen: false },
  { id: 2, label: "Träna", isGreen: false },
  { id: 3, label: "Programmera", isGreen: false }
])

const newTodo = ref("")
const save = () => {
  if(newTodo.value.trim() === "") {
    alert("Please enter a task")
    return
  }

  const item = {
    id: items.value.length + 1,
    label: newTodo.value,
    isGreen: false
  }
  items.value.push(item)
  newTodo.value = ""
}

const remove = (item) => {
  items.value = items.value.filter(i => i.id !== item.id)
}

const removeAll = () => {
  items.value = []
}

const done = (item) => {
  item.isGreen = !item.isGreen
}
</script>

<template>
  <div class="container">
    <header>
      <h1>
        <span class="icon-text">
          <IconTodo/>
          {{ header }}
        </span>
      </h1>
    </header>

    <main>
      <div class="main-area">
        <div class="input-area">
          <input v-model="newTodo" placeholder="Add task" />
          <button @click="save">Save</button>
          <button @click="removeAll">Remove All</button>
        </div>

        <ul class="todo-list">
          <li v-for="(item, index) in items" :key="item.id" @click="done(item)" :class="{ green: item.isGreen }">
            <div class="todo-item">
              <span>{{ item.label }}</span>
              <button @click.stop="remove(item)">Remove</button>
            </div>
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

header {
  text-align: center;
  margin-bottom: 20px;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
}

.icon-text {
  display: flex;
  flex-direction: row;
  align-items: center;
  color: #007bff;
}

.icon-text svg {
  margin-right: 10px;
}

.main-area {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  color: #333;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
  background-color: #f1f1f1;
}

.todo-item:hover {
  background-color: #e9e9e9;
}

.green {
  color: DBE6EA;
}
</style>