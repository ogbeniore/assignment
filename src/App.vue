<template>
  <div id="app">
    <h1>Best Movies</h1>
    <div class="search_form">
      <form @submit.prevent="search">
        <input type="text" name="search" v-model="searchItem" class="form_item">
        <button class="form_button" type="submit">
          Search
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
import { setTimeout } from 'timers';
export default {
  name: "app",
  components: {
    MovieCard,
  },
  data() {
    return {
      movieList: [
        {
          Name: "John Frusciante",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Reservoir Dogs",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Foo Fighters",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Pearl Jam",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Sublime",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Inglourious Basterds",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Incubus",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Audioslave",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Jackie Brown",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Nirvana",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "The Big Lebowski",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Goodfellas",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Guns N' Roses",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Death Proof",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "The Offspring",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Django Unchained",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Rage Against The Machine",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Snatch",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Trainspotting",
          Type: "movie",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        },
        {
          Name: "Weezer",
          Type: "music",
          Url:
            "http://static.tvmaze.com/uploads/images/original_untouched/60/151357.jpg"
        }
      ],
      searchItem: '',
      searchResults: [],
      isLoading: true
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
      this.movieList = this.movieList.filter(function (movie) {
        return movie.Name !== name
      })
      this.searchResults = this.searchResults.filter(function (movie) {
        return movie.Name !== name
      })
    }
  },
  mounted() {
    setTimeout(() => {this.isLoading = false}, 5000)
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
.form_item {
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
</style>
