<template>
  <div>
    <div class="player-container">
      <div>
        <h2 class="player1-name">Player1</h2>
        <div>
          <img class="small-image" v-if="player1Choice === 'Rock'" src="./ph/rk_L.png"   alt="ค้อน" />
          <img class="small-image" v-if="player1Choice === 'Paper'" src="./ph/pp_L.png" alt="กระดาษ" />
          <img class="small-image" v-if="player1Choice === 'Scissors'" src="./ph/sc_L.png" alt="กรรไกร" />
        </div>
        <div>
           <h3>Choose:</h3> {{ player1Choice }}
        </div>
        <div>
          <h3>Result:</h3> {{ gameResult1 }}
        </div>
      </div>

      <div>
        <h2 class="player2-name">Player2</h2>
        <div>
          <img class="small-image" v-if="player2Choice === 'Rock'" src="./ph/rk_R.png" alt="ค้อน" />
          <img class="small-image" v-if="player2Choice === 'Paper'" src="./ph/pp_R.png" alt="กระดาษ" />
          <img class="small-image" v-if="player2Choice === 'Scissors'" src="./ph/sc_R.png" alt="กรรไกร" />
        </div>
        <div>
          <h3>Choose:</h3> {{ player2Choice }}
        </div>
        <div>
          <h3>Result:</h3> {{ gameResult2 }}
        </div>
      </div>

    </div>

    <div>
      <button @click="playRound" class="round-button">Play</button>
      <button @click="resetGame" class="reset-button">Re-Pley</button>
    </div>

    <div class="score-container"> 
    <h2 class="score-text">Point {{ player1Score }} : {{ player2Score }}</h2> </div>
  </div>
</template>

<style>
img {
    width: 100px; 
    height: auto; 
  }
</style>



<script>
import { ref } from 'vue';

export default {
  data() {
    return {
      player1Score: 0,
      player2Score: 0,
      gameResult1: '',
      gameResult2: '',
      player1Choice: '', 
      player2Choice: '', 
      choices: ['Rock', 'Paper', 'Scissors'],
    };
  },
  methods: {
  playRound() {
    const player1Index = Math.floor(Math.random() * this.choices.length);
    const player2Index = Math.floor(Math.random() * this.choices.length);

    const player1Choice = this.choices[player1Index];
    const player2Choice = this.choices[player2Index];

    if (player1Choice === player2Choice) {
      this.gameResult1 = 'Draw';
      this.gameResult2 = 'Draw';
    } else if (
      (player1Choice === 'Rock' && player2Choice === 'Scissors') ||
      (player1Choice === 'Paper' && player2Choice === 'Rock') ||
      (player1Choice === 'Scissors' && player2Choice === 'Paper')
    ) {
      this.gameResult1 = 'Win';
      this.gameResult2 = 'Lose';
      this.player1Score++;
    } else if (
      (player1Choice === 'Scissors' && player2Choice === 'Rock') ||
      (player1Choice === 'Rock' && player2Choice === 'Paper') ||
      (player1Choice === 'Paper' && player2Choice === 'Scissors')
    ) {
      this.gameResult1 = 'Lose';
      this.gameResult2 = 'Win';
      this.player2Score++;
    }
    this.player1Choice = player1Choice;
    this.player2Choice = player2Choice;
  },
  resetGame() {
    this.player1Score = 0;
    this.player2Score = 0;
    this.gameResult1 = '';
    this.gameResult2 = '';
    this.player1Choice = '';
    this.player2Choice = '';
    },
  },
};

</script>
