<template>
    <div class="container" :key='item.id' >
        <div class="added_fields">
            <input type="checkbox" :id="item.id" :name="item.id" class="rdo_btns"  @change.prevent="onChange($event, item)" :checked="isChecked(item)"/>
            <label htmlFor="first_radio">{{ item.name }}</label>
        </div>
        <button @click="crossClick(item)">x</button>
    </div>
</template>

<script setup>
import { ref, defineProps,defineEmits } from "vue";
const emit = defineEmits(["updatedTodo","deleteTodo"]);
const props = defineProps({
    item: Object
});
const crossClick = (item) => {
    emit('deleteTodo',item)
}

const isChecked = (data) => {
   return data && data?.status==='completed'?true:false;
};

const onChange = (event, item) => {
  if(event.target.checked ===true){
    item.status='completed'
    emit('updatedTodo',item)
  }else{
    item.status='active'
    emit('updatedTodo',item)
  }

}


</script>
<style scoped>
.container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-top: 0.5px solid rgb(235, 228, 228);
    width: 100%;
}

.added_fields {
    
    padding: 14px;
    font-size: 18px;
    position: relative;
}
button{
    margin-right: 20px;
}
</style>