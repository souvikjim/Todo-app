<template>
    <div className="footer">
        <div className="count">
            <p>{{ remainingItems }} items left</p>
        </div>
        <div className="footer_button">
            <button @click="changeFilterStatus('all')">All</button>
            <button @click="changeFilterStatus('active')">Active</button>
            <button @click="changeFilterStatus('completed')">Completed</button>
        </div>
        <div className="completed_item">
            <button @click="clearCompleted">Clear Completed</button>
        </div>
    </div>
</template>

<script setup>

import { ref, defineProps,computed,defineEmits } from "vue";

const emit = defineEmits(['filterStatus','clearCompleted'])
const props = defineProps({
  allTodos: Object,
});

const remainingItems = computed(() => {
  return props.allTodos.filter(item => item.status !== 'completed').length;
});
const changeFilterStatus=(e)=>{
    emit('filterStatus',e)
}

const clearCompleted=()=>{
    emit('clearCompleted')
}

</script>

<style scoped>
.footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0px 20px;
    border-top: 0.5px solid rgb(235, 228, 228);
    background-color: beige;
    border-bottom-left-radius:4px ;
    border-bottom-right-radius:4px ;
}

.count {
    color: #b39999;
}

.footer_button>button {
    border: 1px solid white;
    gap: 1rem;
    background-color: #fff;
    margin-right: 7px;
    color: #b39999;
}

.footer_button>button:hover {
    border: 1px solid #b39999;
    border-radius: 5px;
}

.completed_item>button {
    border: 1px solid white;
    gap: 1rem;
    background-color: #fff;
    margin-right: 7px;
    color: #b39999;
}

.completed_item>button:hover {
    border: 1px solid #b39999;
    border-radius: 5px;
}
</style>
