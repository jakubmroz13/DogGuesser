<template>
  <header>
    <div id="logo" @click="playGame = false">DogGuesser</div>
  </header>
  <main>
    <GameComponent v-if="playGame" />
    <HomeComponent v-else @handlePlayGame="this.playGame = true" />
  </main>
</template>

<script>
import HomeComponent from './components/HomeComponent.vue';
import GameComponent from './components/GameComponent.vue';

export default {
  name: 'App',
  components: {
    HomeComponent,
    GameComponent,
  },
  data() {
    return {
      playGame: false,
    }
  },
}
</script>

<style>
body {
  background-color: #22272e;
}

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  color: white;
  font-family: system-ui, -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
    'Helvetica Neue', sans-serif;
}

header {
  padding: 10px;
  background-color: #2d333b;
  display: flex;
  justify-content: center;
  align-items: center;
}

#logo {
  font-size: large;
}

#logo:hover {
  cursor: pointer;
}

main {
  margin-top: 4vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

button {
  border: 0;
  background-color: #636e7b;
  border-radius: 10px;
  padding: 10px;
  font-size: 1.1rem;
}

button:hover {
  background-color: #768390;
  cursor: pointer;
}

img {
  border-radius: 10px;
  max-width: 94vw;
  max-height: 45vh;
}

p {
  padding: 10px;
  margin: 1vh 0;
  text-align: center;
}

#play-btn {
  padding: 12px 30px;
}

@media (min-width: 768px) {
  button {
    font-size: 1.4rem;
  }

  main {
    margin-top: 8vh;
  }
}
</style>
