<script setup>
defineProps({
    msg: {
        type: String,
        required: true
    }
})
</script>
<template>
    <h1> {{ msg }} </h1>
</template>
<style scoped>
h1 {
    font-weight: 900;
    font-size: 2rem;
    padding: 1rem;
}
</style>