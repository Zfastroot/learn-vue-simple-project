<script>
  export default{
    data(){
      return{
        player_1:{
          score:0
        },
        player_2:{
          score:0
        }
      }  
    },
    methods:{
      incScore(player){
        player.score++;
      },
      decScore(player){
        if(player.score>0){
          player.score--;
        }
      }  
    }
  }
  

</script>

<template>
  <div id="app">
    <h1 class="text-center">Player Score Counter</h1>
    <div class="card">
      <div class="card-body text-center">
        <h3>Player 1</h3>
        <button type="button" class="btn btn-danger" @click="decScore(player_1)">Down</button>
        <span class="player-score">{{ player_1.score }}</span>
        <button type="button" class="btn btn-success"  @click="incScore(player_1)">Up</button>
      </div>
      <div class="card-body text-center">
        <h3>Player 2</h3>
        <button type="button" class="btn btn-danger" @click="decScore(player_2)">Down</button>
        <span class="player-score">{{ player_2.score }}</span>
        <button type="button" class="btn btn-success"  @click="incScore(player_2)">Up</button>
      </div>
    </div>
  </div>
</template>

<style>
  .player-score{
    font-size: 4rem;
    margin: 10px;
  }
</style>
