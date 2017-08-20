<template>
  <div id="app">
    {{ msg }}
    <ul>
      <li v-for="film in films">{{ film.name }}</li>
    </ul>
    <div class="add-container">
      <input v-model:value="input" type="text"></input>
      <button v-on:click="suggestFilm">Suggest</button>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'

let config = {
  apiKey: "AIzaSyAKbVGMzUaOLXNUE_6XB9_KBz7iPhkbE5Y",
  authDomain: "film-hopper.firebaseapp.com",
  databaseURL: "https://film-hopper.firebaseio.com",
  projectId: "film-hopper",
  storageBucket: "film-hopper.appspot.com",
  messagingSenderId: "1055567035486"
}

let app = Firebase.initializeApp(config)
let db = app.database();

let filmsRef = db.ref('films')

export default {
  name: 'app',
  firebase: {
    films: filmsRef
  },
  
  data () {
    return {
      msg: 'These are films Bryan has in the hopper...',
      input: '',
    }
  },

  methods: {
    suggestFilm() {
      if (this.input) {
        this.$firebaseRefs.films.push({
          name: this.input
        })
        this.input = ''
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
  display: block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

export default 