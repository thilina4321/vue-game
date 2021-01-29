<template>
  <div class="player">
    <h2>{{ names[0] }}</h2>
    <h3 :style="{ width: monsterHealth  +'%' }" class="life"></h3>
  </div>
  <div class="player">
    <h2>{{ names[1] }}</h2>
    <h3 :style="{ width: playerHealth + '%' }" class="life"></h3>
  </div>
  <div class="main__btn" v-if="!winner">
    <div class="btn">
      <button @click="attackToMonster">Attack</button>
      <button :style="{ backgroundColor: canUseSpecialAttack ? 'grey':'purple' }"
       :disabled="canUseSpecialAttack" @click="specialAttack">Special Attack</button>
    </div>

    <div class="btn">
      <button @click="surrender">Surrender</button>
    </div>
    
  </div>
  <div class="over" v-if="winner">
      <h2> {{winner}} </h2>
      <button @click="startAgain">Start Again</button>
    </div>
</template>

<script>
export default {
  data() {
    return {
      names: ["Monster Health", "Player Health"],
      playerHealth: 100,
      monsterHealth: 100,
      round:0,

      winner:null
    };
  },
  computed:{
    canUseSpecialAttack(){
      return this.round % 3 != 0
    }
  },
  watch:{
    playerHealth(value){
      if(this.playerHealth <= 0 && this.monsterHealth <= 0){
        this.winner = 'draw'
      }else if(value <= 0){
        this.winner = 'Monster wins'
      }
    },
    monsterHealth(value){
      if(this.playerHealth <= 0 && this.monsterHealth <= 0){
        this.winner = 'draw'
      }else if(value <= 0){
        this.winner = 'Player wins'
      }
    },
  },
  methods: {
    surrender(){
this.winner = 'monsater wins'
    },
    startAgain(){
      this.winner = null
      this.playerHealth = 100
      this.monsterHealth = 100
      this.round = 0
    },
    attackToPlayer() {
      const attack = Math.floor(Math.random() * 7) + 5;
      this.playerHealth -= attack;
    },

    attackToMonster() {
      this.round++
      const attack = Math.floor(Math.random() * 7) + 8;

      this.monsterHealth -= attack;
      this.attackToPlayer();
    },

    specialAttack(){
      this.round++
      const attack = Math.floor(Math.random() * 15) + 10
      this.monsterHealth -= attack
      this.attackToPlayer()
    }
  },
};
</script>

<style scoped>
.player {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 80%;
  margin: 10px auto;
  box-shadow: 0 1px 1px black;
  margin-bottom: 10px;
}
.over{
  widows: 50%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  box-shadow: 0 1px 1px black;
}
h3 {
  height: 30px;
  width: 100%;
  background-color: green;
  align-self: flex-start;
}
.btn {
  display: flex;
}
button {
  margin: 10px 40px;
  background-color: purple;
  color: white;
  padding: 20px;
  border-radius: 10px;
}
button:focus {
  outline: none;
}
.main__btn {
  display: flex;
  flex-direction: column;
}
</style>