<script setup>
import inputBox from '@/components/inputBox.vue'
import card from "@/components/card.vue"
import options from "@/components/footer.vue"
import { ref, watch } from 'vue'
let allTodos = ref('allTodos' in sessionStorage && sessionStorage.getItem("allTodos") ? JSON.parse(sessionStorage.getItem("allTodos")) : [])
let visibleTodos = ref([])
let filteredStatus = ref('')

const showTask = (e) => {
  if (e.name.trim() !== '') {
    allTodos.value.push(e)
    sessionStorage.setItem("allTodos", JSON.stringify(allTodos.value))
  }
}
const updateTodoList = (item) => {
  const replaceIndex = allTodos.value.findIndex(obj => obj.id === item.id);
  if (replaceIndex !== -1) {
    allTodos.value[replaceIndex] = item
    sessionStorage.setItem("allTodos", JSON.stringify(allTodos.value))
  }
}
const deleteTodo = (item) => {
  allTodos.value = allTodos.value.filter(todo => todo.id !== item.id);
}
const changeFilterStatus = (filterStatus) => {
  filteredStatus.value = filterStatus;
}
watch([filteredStatus, allTodos], () => {
  let tempAllTasks = [...allTodos.value];
  if (filteredStatus.value !== 'all') {
    tempAllTasks = allTodos.value.filter(task => task.status === filteredStatus.value);
  }
  visibleTodos.value = tempAllTasks;
  console.log('visibleTodos.value :>> ', visibleTodos.value);
}, { deep: true });
const clearCompleted = () => {
  allTodos.value = allTodos.value.filter(item => item.status !== 'completed');
}
</script>

<template>
  <div class="container">
    <div class="semiContainer">
      <inputBox @newTask="showTask" />
      <div class="cardHolder">
        <card v-for="todo in visibleTodos" :key="todo.id" :id="todo.id" :item="todo" @updatedTodo="updateTodoList"
          @deleteTodo="deleteTodo" />
      </div>
      <options :allTodos="allTodos" @filterStatus="changeFilterStatus" @clearCompleted="clearCompleted" />
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 500px;
  margin: 0 auto;
}

.semiContainer {
  width: 100%;
}

.cardHolder {
  overflow-x: hidden;
  margin-top: 10px;
  max-height: 500px;
  border-bottom: 1px solid black;
}
</style>