<template>
    <div class="container mt-5">
        <h1>Todo List</h1>
        <AddItem v-on:getlist="getItems" />
        <Items :items="items" v-on:delete="getItems" class="mt-3" />
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Items from './components/Items.vue'
import AddItem from './components/AddItem.vue'

const items = ref([])

const getItems = () => {
    axios.get('http://127.0.0.1:8000/api/item').then(response => {
        console.log(response.data)
        items.value = response.data.data;
    }).catch(err => console.log(err));
}

onMounted(() => {
    getItems()
})

</script>

<style scoped>
.container {
    width: 600px;
    margin: auto;
}
</style>
