<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Block from './components/BlockComponent.vue'
import Result from './components/ResultComponent.vue'

const isPlaying = ref(false)
const delay = ref(null)
const score = ref(null)
const showResult = ref(false)

function startGame() {
  isPlaying.value = true
  showResult.value = false
  delay.value = 2000 + Math.random() * 4000
}

function endGame(reactionTimer) {
  score.value = reactionTimer
  isPlaying.value = false
  showResult.value = true
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Reaction Timer" />
    </div>
  </header>

  <main>
    <Block v-if="isPlaying" :delay="delay" @end-game="endGame" />
    <button @click="startGame" :disabled="isPlaying">Play</button>
    <Result v-if="showResult" :score="score" />

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

button {
  width: 100%;
  background: hsla(160, 100%, 37%, 1);
  color: white;
  border: none;
  border-radius: 5px;
  padding: 8px 16px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
