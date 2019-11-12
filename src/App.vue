<template>
  <div id="app">
    <h1>{{title}}</h1>
    <div class="search_form">
      <form @submit.prevent="search">
        <input type="text" name="search" v-model="searchItem" class="form_item">
        <button class="form_button" type="submit">
          Search
        </button>
      </form>
    </div>
    <div class="movie_form">
      <form @submit.prevent="addMovie">
        <div>
          <label for="name">Name</label>
          <input type="text" name="name" v-model="Name">
        </div>
        <div>
          <label for="type">Type</label>
          <select name="type" v-model="Type">
            <option value="music">Music</option>
            <option value="movie">Movie</option>
          </select>
        </div>
        <div>
          <label for="">Url</label>
          <input type="url" name="url" v-model="Url">
        </div>
        <button class="form_button" type="submit">
          Add movie
        </button>
      </form>
    </div>
    <template v-if="!isLoading">
      <div class="container" v-if="this.searchResults.length != 0 && this.searchItem">
        <MovieCard
          v-for="movie in searchResults"
          :key="movie.Name"
          :movieDetails="movie"
          @delete="deleteMovie(movie.Name)"/>
      </div>
      <div class="container" v-else-if="this.searchResults.length == 0 && this.searchItem">
        <p>No results found</p>
      </div>
      <div class="container" v-else>
        <MovieCard
          v-for="movie in movieList"
          :key="movie.Name"
          :movieDetails="movie"
          @delete="deleteMovie(movie.Name)"/>
      </div>
    </template>
    <div v-else>
      Loading...
    </div>
  </div>
</template>

<script>
import MovieCard from '@/components/ImageCard.vue'
export default {
  name: "app",
  components: {
    MovieCard,
  },
  data() {
    return {
      movieList: [],
      searchItem: '',
      searchResults: [],
      isLoading: true,
      title: 'My movies',
      Name: '',
      Type: '',
      Url: ''
    };
  },
  methods: {
    search() {
      let searchKeyword = this.searchItem.toLowerCase()
      let filteredArray = this.movieList.filter(function (movie) {
        let name = movie.Name.toLowerCase();
        return name.includes(searchKeyword)
      });
      this.searchResults = filteredArray
    },
    deleteMovie(name) {
      this.title = "new title"
      this.movieList = this.movieList.filter(function (movie) {
        return movie.Name !== name
      })
      this.searchResults = this.searchResults.filter(function (movie) {
        return movie.Name !== name
      })
    },
    addMovie() {
      const Data = {
        Name: this.Name,
        Type: this.Type,
        Url: this.Url
      }
      this.$http.post('http://localhost:3000/movies', Data)
        .then(response => {
          this.movieList.push(response.data)
          this.Name = ''
          this.Type = '',
          this.Url = ''
        })
        .catch(error => console.log(error.response))
    }
  },
  mounted() {
    this.$http.get('http://localhost:3000/movies')
      .then(response => {
        this.isLoading = false;
        this.movieList = response.data
      })
      .catch(error => {
        console.log(error.response)
      })
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search_form {
  width: 100%;
  padding: 1rem 2.75rem;
  box-shadow: 0 2px 2px rgba(0,0,0,0.2);
  margin: 0 auto;
}
form {
  display: flex;
  margin: 0 auto;
  max-width: 700px;
}
.form_item,
input,
select {
  padding: 1rem;
  font-size: 18px;
  border: 1px solid blueviolet;
  border-radius: 50px;
  margin-right: 2rem;
  flex: 1;
}
.form_button {
  background: blueviolet;
  color: aliceblue;
  border-radius: 50px;
  padding: 1rem 3rem;
  font-size: 18px;
  cursor: pointer;
}
.form_button:focus,
.form_item:focus {
  outline: 0;
  box-shadow: 1px 1px 10px blueviolet
}
.container {
  max-width: 800px;
  margin: 3rem auto;
  padding: 2rem;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;
}
.movie_form form {
display: block;
}
form > div {
  margin: 1rem;
}
</style>
