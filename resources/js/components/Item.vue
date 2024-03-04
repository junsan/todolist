<template>
    <li>
        <input :onchange="completeItem" type="checkbox" v-model="completed.is_completed" /> 
        <span :class="item.is_completed ? 'completed': ''">{{ item.name }}</span> <button @click="deleteItem">delete</button>
    </li>
</template>

<script setup>
import { reactive } from 'vue'

const props = defineProps({
    item: {
        type: Object
    }
})

const completed = reactive({
    is_completed: props.item.is_completed ? true : false
})

const emit = defineEmits(['delete'])

const deleteItem = () => {
    axios.delete(`http://127.0.0.1:8000/api/item/${props.item.id}`)
    emit('delete')
}

const completeItem = () => {
    axios.patch(`http://127.0.0.1:8000/api/item/${props.item.id}`, completed)
    emit('delete')
}

</script>

<style scoped>
    .completed {
        text-decoration: line-through;
    }
</style>