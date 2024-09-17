<script setup>
import { ref } from 'vue'
import IconTodo from "@/components/icons/IconTodo.vue";

const header = ref('My ToDo-list')
const items = ref([
  { id: 1, label: "Frukost", isDone: false },
  { id: 2, label: "Träna", isDone: false },
  { id: 3, label: "Programmera", isDone: false }
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
  item.isDone = !item.isDone
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
          <li v-for="(item, index) in items" :key="item.id" @click="done(item)" :class="{ done: item.isDone }">
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
  .done {
    color: #b3b4b8;
    text-decoration: line-through;
  }
</style>