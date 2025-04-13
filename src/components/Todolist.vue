<script setup>
import { ref, computed } from 'vue'
import IconTodo from "./icons/IconTodo.vue";
import vFocus from '../directives/v-focus.js';

const header = ref('My ToDo-list')
const items = ref([
  { id: 1, label: "Äta Frukost", isDone: false },
  { id: 2, label: "Träna", isDone: false },
  { id: 3, label: "Programmera", isDone: false }
])

const newTodo = ref("")
const showDone = ref(true) // Show done items

const filteredItems = computed(() => {
  return items.value.filter(item => showDone.value || !item.isDone)
})

const save = () => {
  if(newTodo.value.trim() === "") {
    alert("Please enter a task")
    return
  }

  const item = {
    id: items.value.length + 1,
    label: newTodo.value,
    isDone: false
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
          <input v-model="newTodo" v-focus placeholder="Add task" />
          <button @click="save">Save</button>
          <button @click="removeAll">Remove All</button>
        </div>
        <div>
          <input type="checkbox" v-model="showDone" id="showDone" />
          <label for="showDone">Show Done Items</label>
        </div>

        <ul class="todo-list">
          <li v-for="(item, index) in filteredItems" :key="item.id" @click="done(item)" :class="{ done: item.isDone }">
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

