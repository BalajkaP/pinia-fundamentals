<script setup>
import { useTodoListStore } from "@/stores/todoList"
import { storeToRefs } from "pinia"

const store = useTodoListStore()

// storeToRefs lets todoList keep reactivity:
// Here, storeToRefs(store) returns an object containing reactive references. The destructuring extracts the todoList property (co je uvnitř state) from that object. It's equivalent to:
// const storeRefs = storeToRefs(store)
// const todoList = storeRefs.todoList
const { todoList } = storeToRefs(store)

// destructuring action method doesn't require using storeToRefs:
//Here, you're destructuring directly from the store object to extract the toggleCompleted method. It's equivalent to:
// const toggleCompleted = store.toggleCompleted
const { toggleCompleted } = store
</script>

<template>
  <div
    v-for="todo in todoList"
    :key="todo.id"
    class="list"
  >
    <!-- Zde zobrazuji jednotlivé todo položky v rámci for cyklu -->
    <div class="item">
      <!-- Jde zde o dynamicky definovaný class=> :class -->
      <span :class="{ completed: todo.completed }">{{ todo.item }}</span>
      <!-- Ten &#10004; je kód pro checkmark. Po klik se přeškrtne -->
      <span @click.stop="toggleCompleted(todo.id)">&#10004;</span>
    </div>
  </div>
</template>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
