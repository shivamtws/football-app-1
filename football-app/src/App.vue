<template>
  <div id="app">
    <FootballApp />
  </div>
</template>

<script>
import FootballApp from './components/FootballApp.vue'; // Importing the FootballApp component

export default {
  name: 'App', // Our main Vue component's identifier
  components: {
    FootballApp // Registering the FootballApp component
  }
};
</script>
