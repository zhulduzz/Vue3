<script setup>
import { ref, computed } from 'vue'

//App.mount('#app')
//App.component('TodoDeleteButton', TodoDeleteButton)
//App.component('TodoFilterButton', TodoFilterButton)
//App.component('TodoMark', TodoMark)
//App.component('TodoAddTasks', TodoAddTasks)

const tasks = ref([
  { text: "enter your task", done: false, category: "Tasks" }
])


const newTask = ref("")


const incompleteCount = computed(() =>
  tasks.value.filter(task => !task.done).length
)


const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push({
      text: newTask.value,
      done: false,
      category: "General"
    })
    newTask.value = ""
  }
}


const toggleTask = (index) => {
  tasks.value[index].done = !tasks.value[index].done
}

</script>

<template>
  
  <span style="color:aquamarine; font-size: 10;">To do list app</span>
  <h2 style="font-size: 10; font-weight: 100;">Невыполненные задачи: {{ incompleteCount }}</h2>

  <div id="app">
    <button @click="count++"> {{ count }}</button>
  </div>

  
  <input v-bind:size=40 style="font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;font-style: italic;" v-model="newTask" placeholder="Введите задачу" />
  <button style="color: aquamarine; background-color: beige;font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;" @click="addTask">Добавить</button>

  
  <p v-if="tasks.length === 0">Нет задач</p>

  
  <ul v-else>
    <li v-for="(task, index) in tasks" :key="index"
        :class="{ completed: task.done }">
      <span class="tasks">{{ task.text }}</span>
      <button style="color: aquamarine; background-color: beige;font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;" @click="toggleTask(index)">
        {{ task.done ? "Отменить" : "Сделано" }}
      </button>
    </li>
  </ul>
</template>

<style>
.completed {
  text-decoration: line-through;
  color: rgb(226, 137, 137);
  font-size: medium;
  font-style: italic;
}

.button{
  color:aquamarine

}
.tasks{
  color: #65cf9e;
  font-size: 10;
  font-weight: 5;
  size: 0cap;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  
}
</style>





