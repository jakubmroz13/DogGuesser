<template>
  <div id="statistics">
    <div id="hearts">
      <div v-for="n in hearts" :key="n" class="heart"></div>
    </div>
    <div id="score">{{ score }}</div>
  </div>
</template>
<script>
export default {
  name: 'StatisticsComponent',
  props: {
    hearts: Number,
    score: Number,
  },
}
</script>
<style scoped>
#statistics {
  width: min(92vw, 1000px);
  margin-bottom: 2vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.hearts {
  display: flex;
  justify-content: center;
  align-items: center;
}

.heart {
  background-color: rgb(255, 83, 83);
  display: inline-block;
  height: 20px;
  margin: 0 10px;
  position: relative;
  top: 0;
  transform: rotate(-45deg);
  width: 20px;
}

.heart:before,
.heart:after {
  content: "";
  background-color: rgb(255, 83, 83);
  border-radius: 50%;
  height: 20px;
  position: absolute;
  width: 20px;
}

.heart:before {
  top: -10px;
  left: 0;
}

.heart:after {
  left: 10px;
  top: 0;
}

#score {
  font-size: xx-large;
}
</style>