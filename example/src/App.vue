<template>
  <div id="app">
    <calendar :events="events"></calendar>
  </div>
</template>

<script>
import Calendar from '../../components/buefy-calendar';

export default {
  name: 'app',
  components: {
    'calendar': Calendar
  },
  data() {
      return {
          events: {
              "2017-06-02": [
                  { title: "Rehearsal", url: "http://www.google.com" }
              ]
          }
      }
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
