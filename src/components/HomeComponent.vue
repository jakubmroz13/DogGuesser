<template>
  <h1 id="welcome-text">Welcome</h1>
  <img v-if="welcomeImage" :src="welcomeImage" alt="dog" />
  <div v-else id="loading">Loading...</div>
  <p>Let's see if you can guess some dog breeds</p>
  <button id="play-btn" @click="$emit('handlePlayGame')">Play</button>
</template>
<script>
export default {
  name: 'HomeComponent',
  data() {
    return {
      welcomeImage: null,
    }
  },
  mounted() {
    const API = 'https://dog.ceo/api/breeds/image/random';
    fetch(API)
      .then((res) => res.json())
      .then((data) => this.welcomeImage = data.message)
      .catch((error) => console.log(error));
  },
}
</script>
<style scoped>
#welcome-text {
  margin-bottom: 1vh;
}

#loading {
  margin: 50px;
}
</style>