<template>
  <div id="app">
    <div>
      <div class="">
        <input type="text" v-model="search">
      </div>

      <div v-for=" movie  in listaMovie" :key="movie.id">
        <div>
          {{ movie.title}}
        </div>
        
      </div>
    </div>
    
  </div>
</template>

<script>


import axios from 'axios'

export default {
  name: 'App',
  components: {
    
  },
  data(){
    return{
      search: 'batman',
      listaMovie: [],
      baseURL: 'https://api.themoviedb.org/3'
    }
  },
  created() {
    /* axios.get(`https://api.themoviedb.org/3/search/movie?api_key=f1a4307ca5d0830b05b752ed609bbbb0&query=${ this.search}` */
    axios.get(`${this.baseURL}/search/movie`,{
      params: {
        api_key: 'f1a4307ca5d0830b05b752ed609bbbb0',
        query: this.search,
        language: 'it-IT'
      }
    })
    .then( res => {
        this.listaMovie = res.data.results
      })

      
  }
  
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
