<template>
    <ul>
        <Item v-for="item in items" :key="item.id" :item="item" v-on:delete="deleteItem" />
    </ul>
</template>

<script setup>
import Item from './Item.vue';

const props = defineProps({
    items: {
        type: Array
    }
})

const emit = defineEmits(['delete'])

const deleteItem = () => {
    emit('delete')
}

</script>