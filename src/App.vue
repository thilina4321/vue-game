<template>
  <div class="main">
    <h1>Monster Slayer</h1>
    <player-life />
  </div>
</template>

<script>

  import PlayerLife from './components/PlayerLife'
export default {
  components:{
    PlayerLife
  }
};
</script>

<style scoped>
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
h1 {
  width: 100%;
  background-color: brown;
  color: white;
  padding: 10px;
  margin: 0;
  text-align: center;
}
</style>