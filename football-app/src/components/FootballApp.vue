<template>
    <div>
      <table>
        <thead>
          <tr>
            <th>Rank</th>
            <th>Logo</th>
            <th>Team Name</th>
            <th>Form</th>
            <th>Played</th>
            <th>Win</th>
            <th>Draw</th>
            <th>Loss</th>
            <th>Goals For</th>
            <th>Goals Against</th>
            <th>Goal Difference</th>
            <th>Points</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="team in teams" :key="team.idTeam">
            <td>{{ team.intRank }}</td>
            <td><img :src="team.strTeamBadge" alt="Team Logo" class="team-logo" /></td>
            <td>{{ team.strTeam }}</td>
            <td>{{ team.strForm }}</td>
            <td>{{ team.intPlayed }}</td>
            <td>{{ team.intWin }}</td>
            <td>{{ team.intDraw }}</td>
            <td>{{ team.intLoss }}</td>
            <td>{{ team.intGoalsFor }}</td>
            <td>{{ team.intGoalsAgainst }}</td>
            <td>{{ team.intGoalDifference }}</td>
            <td>{{ team.intPoints }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        teams: []
      };
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      async fetchData() {
        try {
          const response = await fetch(
            'https://www.thesportsdb.com/api/v1/json/3/lookuptable.php?l=4328&s=2020-2021'
          );
          const data = await response.json();
          this.teams = data.table;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      }
    }
  };
  </script>
  
  <style>
  /* Add any necessary styles here */
  .team-logo {
    max-width: 30px;
    max-height: 30px;
  }
  </style>
  