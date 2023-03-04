<template>
  <router-link to="/"><p class="back">Back To Jokes</p></router-link>
<div class="center">
    {{ joke.joke }}
    <hr>
    <small>Joke ID: {{ $route.params.id }} </small>
  </div>
</template>

<script>
import axios from 'axios';

  export default {
    data() {
      return {
        joke:[]
      }
    },
    created() {
      axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, {
      headers: {
        'Accept': 'application/json'
      },
    })
    .then(response => {
      this.joke = response.data;
    })
    .catch(error => {
      console.log(error);
    });
    }
  }
</script>

<style scoped>
.center {
  display:grid;
  justify-content:center;
  margin-top:50px;
  line-height: 30px;
}
.back {
  position:relative;
  margin-top:50px;
  left:10%;
  text-decoration: underline;
}
</style>