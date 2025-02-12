<script setup lang="ts">
    import{ref, reactive, computed, watch} from 'vue'

    const button =ref(0)

    function increment(){
        button.value++
    }

</script>

<template>
    <h1>Home</h1>
    <button class="button" @click="increment">Incrémenter</button>
    <p>{{ button }}</p>
</template>