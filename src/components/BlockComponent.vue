<script setup>
import { ref, onMounted } from 'vue';

const showBlock = ref(false)
const timer = ref(null)
const reactionTimer = ref(0)
const backgroundColor = ref(null)
const props = defineProps({
    delay: Number
})

const emit = defineEmits(["endGame"])

function startTimer() {
    timer.value = setInterval(() => {
        reactionTimer.value += 10
    }, 10)
}

function stopTimer() {
    clearInterval(timer.value)
    console.log(reactionTimer.value)
    emit('endGame', reactionTimer.value)
}

onMounted(() => {
    backgroundColor.value = Math.floor(50 + Math.random() * 101)
    console.log(backgroundColor.value)
    setTimeout(() => {
        showBlock.value = true
        startTimer()
    }, props.delay)
})

</script>

<template>
    <div class="block" v-if="showBlock" @click="stopTimer">Click ME!</div>
</template>

<style>
.block {
    width: 400px;
    border-radius: 20px;
    background: hsla(v-bind('backgroundColor'), 100%, 37%, 1);
    color: white;
    text-align: center;
    padding: 120px 0;
    margin: 40px auto;
}
</style>