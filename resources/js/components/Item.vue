<template>
    <li class="list-group-item" :style="item.is_completed ? 'background-color: #eee; color: #ccc': ''">
        <input style="font-size: 18px;" :onchange="completeItem" v-model="completed.is_completed" class="form-check-input me-1" type="checkbox">
        <label style="font-size: 18px; margin-left: 10px;" class="form-check-label" :class="item.is_completed ? 'completed': ''" for="firstCheckbox">{{ item.name }}</label>
        <button @click="deleteItem" style="float: right; border: none;"><i class="bi-trash3" style="font-size: 1rem; color: red;"></i></button>
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
    axios.delete(`http://127.0.0.1:8000/api/item/${props.item._id}`)
    emit('delete')
}

const completeItem = () => {
    axios.patch(`http://127.0.0.1:8000/api/item/${props.item._id}`, completed)
    emit('delete')
}

</script>

<style scoped>
    .completed {
        text-decoration: line-through;
    }
</style>