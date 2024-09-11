<template>
  <div id="app">
    <h1 class="text-center">Cricket Players</h1>
    <div class="container">
      <div class="row">
      
        <div class="col-md-4" v-for="player in batsmen" :key="player.name">
          <div class="card">
            <img :src="player.image" class="card-img-top" :alt="player.name">
            <div class="card-body">
              <h5 class="card-title">{{ player.name }}</h5>
              <p class="card-text">Matches: {{ player.matches }}</p>
              <p class="card-text">Runs: {{ player.runs }}</p>
              <p class="card-text">50/100: {{ player['50s'] }}/{{ player['100s'] }}</p>
              <p class="card-text">Highest Score: {{ player.highest_score }}</p>
              <p class="card-text">Team Name: {{ player.team_name }}</p>
              <p class="card-text">Best Bowling Figures: {{ player.best_bowling_figures }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      players: [],
      batsmen: [],
    };
  },
  created() {
    fetch("./assets/players.json")
      .then((response) => response.json())
      .then((data) => {
        this.players = data.originalPlayers;
        this.categorizePlayers();
      });
  },
  methods: {
    categorizePlayers() {
     
      this.batsmen = this.players.filter((player) => player.role === 2);
    },
  },
};
</script>

<style>
.container {
  margin-top: 50px;
}

.card {
  margin-bottom: 20px;
}
</style>
