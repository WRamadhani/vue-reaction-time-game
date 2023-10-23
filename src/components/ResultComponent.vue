<script setup>
import { ref } from 'vue';
import { onMounted } from 'vue';

const rank = ref(null)

const props = defineProps({
    score: Number
})

onMounted(() => {
    if (props.score < 250) {
        rank.value = '⚡'
    } else if (props.score < 400) {
        rank.value = '🐱‍👤'
    } else {
        rank.value = '🐢'
    }
})
</script>

<template>
    <p>Reaction Time : {{ props.score }} ms</p>
    <p class="rank">{{ rank }}</p>
</template>

<style>
.rank {
    font-size: 1.4em;
    color: aqua;
    font-weight: bold;
}
</style>