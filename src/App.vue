<template>
  <div id="app">
    <div>
      <div class="header">
        <div class="centroheader">
            <h1>BOOLFLIX</h1>
            <div>
              <input type="text" v-model="search" @keyup.enter="fechData">
              <button>Cerca</button>
            </div>
        </div>
      </div>

      <div v-for=" movie  in listaMovie" :key="movie.id">
        <img :src="movie.poster_path" alt="">
        <div>
          <h3>{{ movie.title }}</h3>
          <span>{{movie.original_title}}</span> -
          <span>{{movie.original_language }}</span>
          <p>Voto: {{ movie.vote_average }}</p>
        </div>
        
      </div>
    </div>

    <MyMain />
    
  </div>
</template>

<script>


import axios from 'axios'

import MyMain from './components/MyMain'

export default {
  name: 'App',
  components: {
    MyMain,
  },
  data(){
    return{
      search: '',
      listaMovie: [],
      baseURL: 'https://api.themoviedb.org/3'
    }
  },
  methods: {
    fechData: function(){
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
  /* created() {
                      verisone intera v
    ..... axios.get(`https://api.themoviedb.org/3/search/movie?api_key=f1a4307ca5d0830b05b752ed609bbbb0&query=${ this.search}` .....

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

      
  } */
  
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.centroheader{
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 0 auto;
  width: 85%;
  height: 100%;
}
.header{
  width: 100%;
  height: 12vh;
  background-color: #161718;
  

    h1{
      color: red;
    }
   
    input{

    }
}
</style>
