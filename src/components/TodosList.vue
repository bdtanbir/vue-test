<template>
    <li>
        {{todo.title}} <button @click="$emit('remove')">Remove</button>
    </li>
</template>

<script>
export default {
    props: ['todo'],
    emits: ['remove']
}
</script>

<style>

    
</style>