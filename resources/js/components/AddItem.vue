<template>
    <div>
        <input type="text" v-model="newItem.name" /> &nbsp; 
        <button @click="addItem" style="border: none;"><i class="bi bi-plus-square-fill" style="font-size: 25px;"></i></button>
    </div>
</template>
<script setup>
import { reactive } from 'vue'

const newItem = reactive({
    name: ''
})

const emit = defineEmits(['getlist'])

const addItem = () => { 
    console.log(newItem)
    axios.post('http://127.0.0.1:8000/api/item', newItem).then(response => {
        emit('getlist')
        newItem.name = ''
    }).catch(err => console.log(err));
}

</script>