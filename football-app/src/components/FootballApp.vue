<template>
    <div class="container">
        <table class="table table-borderless">
            <thead>
                <tr>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th>Form</th>
                    <th>GP</th>
                    <th>W</th>
                    <th>D</th>
                    <th>L</th>
                    <th>GF</th>
                    <th>GA</th>
                    <th>GD</th>
                    <th>Pts</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="team in displayedTeams" :key="team.teamid">
                    <td>{{ team.intRank }}</td>
                    <td><img :src="team.strTeamBadge" alt="Team Logo" class="team-logo" /></td>
                    <td>{{ team.strTeam }}</td>
                    <td>
                        <span v-for="(result, index) in team.strForm" :key="index" :class="{
                            'fas fa-check text-success': result === 'W',
                            'fas fa-times text-danger': result === 'L',
                            'fas fa-minus text-secondary': result === 'D'
                        }" :style="{
    backgroundColor: result === 'W' ? 'green' : result === 'L' ? 'red' : 'gray',
    padding: '10px',
    borderRadius: '100%',
    marginRight: '10px',
}"></span>
                    </td>
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
            displayedTeams: []
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
                this.displayedTeams = data.table;
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
  