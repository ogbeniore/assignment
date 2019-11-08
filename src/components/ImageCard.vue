<template>
  <div class="movie_card">
    <div class="movie_card_image">
      <img :src="movieDetails.Url" :alt="movieDetails.Name+movieDetails.Type">
    </div>
    <div class="movie_card_content">
      <h3>{{ movieDetails.Name }}</h3>
      <p>{{ movieDetails.Type }}</p>
      <button @click="deleteItem">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieCard',
  props: {
    movieDetails: Object,
  },
  methods: {
    deleteItem() {
      this.$emit('delete')
    }
  }
}
</script>

<style scoped>
.movie_card {
  max-width: 100%;
  box-shadow: 0 2px 2px rgba(0,0,0,0.2);
}
.movie_card_image {
  max-height: 200px;
  width: 100%;
  overflow: hidden;
}
.movie_card_image:hover > img {
  filter: grayscale(0);
  cursor: pointer;
}
img {
  width: 100%;
  height: auto;
  object-fit: contain;
  filter: grayscale(0.5);
  transition: all 300ms ease-in-out;
}
.movie_card_content {
  text-align: left;
  border-top: 2px solid blueviolet;
  padding-top: 1.5rem;
  display: flex;
  flex-direction: column;
}
h3 {
  font-weight: 800;
  color: blueviolet;
}
h3, p {
  padding: 0 1rem; 
}
button {
  width: 100%;
  border: none;
  padding: 1rem;
  background: blueviolet;
  color: #ffffff;
  margin-top: auto;
}
</style>