<template>
  <div id="summary">
    <h1 v-if="score > 9">Awesome!</h1>
    <h1 v-else-if="score > 4">Well Done!</h1>
    <h1 v-else-if="score > 2">Not so bad</h1>
    <h1 v-else>Train a bit more</h1>
    <p>You guessed {{ this.score }} {{ this.score > 1 || !this.score ? 'breeds' : 'breed' }}</p>
    <button @click="$emit('handlePlayAgain')">Play Again</button>
  </div>
</template>
<script>
export default {
  name: 'SummaryComponent',
  props: {
    score: Number,
  },
}
</script>
<style scoped>
#summary {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>