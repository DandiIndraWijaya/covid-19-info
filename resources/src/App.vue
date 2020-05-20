<template>
  <div id="app">
    <div class="navbar">
        <center>
          <h2 class="app-title">COVID-19 INFO</h2>
        </center>
      </div>

    <div id="content">
      <div class="left">
        <div class="list-countries">
          <ListCountries />
        </div>
      </div>

      <div class="right">
          <Statistics />
      </div>
    </div>
  </div>
</template>

<script>
import ListCountries from './components/ListCountries.vue'
import Statistics from './components/Statistics.vue'

export default {
  name: 'App',
  components:{
    ListCountries,
    Statistics
  },
}
</script>

<style>
body{
     margin:0px;
     overflow:hidden;
}

#app{
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
     color: #2c3e50;
     padding:0px;
     width:100%;
     margin: 0px;
}

#content{
  width: 100%;
  padding: 0px;
  margin: 0;
  display: flex;
}

.navbar{
  width: 100%;
  height: 50px;
  border-bottom: 1px gainsboro solid;
  margin: 0px;
}

.left{
  width: 200px;
  
}

.right{
  width: 100%;
  height: 100vh;
  background-color: gainsboro;
}

.list-countries{
  overflow-y: scroll;
  overflow-x: hidden;
  height: 90vh;
}


/* width */
::-webkit-scrollbar {
  width: 1px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f7f7f7;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>