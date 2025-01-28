<template>
    <form @submit.prevent='addTask' class="container">
        <input type="text" id="newTask" name="newTask" v-model="newTask" placeholder="Add a new task here">
        <button type="submit">Add</button>
    </form>
</template>
<script>
import { ref } from "vue"
export default {
    setup(props, context) {
        const newTask = ref('');
        const addTask = () => {
            const tempTodo = {
                name: newTask.value,
                id: Date.now(),
                status: 'active'
            }
            context.emit('newTask', tempTodo)
            newTask.value = ''
        }
        return {
            newTask,
            addTask
        }
    }


}



</script>
<style scoped>
.container {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

input {
    border: 1px solid black;
    border-radius: 4px;
    width: 410px;
    padding: 10px;
}

button {
    border: 1px solid black;
    border-radius: 4px;
    background-color: white;
    color: black;
    width: 50px;
    padding: 10px;
}

button:hover {
    border: 1px solid transparent;
    color: white;
    background-color: green;
}
</style>