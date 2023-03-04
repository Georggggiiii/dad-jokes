<template>
  <div class="center">
   <input v-model="searchTerm" @input="onInput" />
    <JokesComp v-for="joke in jokes" :key="joke.id" :joke="joke" />
  </div>
</template>

<script>
import axios from 'axios';

import JokesComp from '@/components/JokesComp.vue'

export default {
  name: 'HomeView',
  data() {
    return {
      jokes: [],
      searchTerm:'',
      timeout: null
    }
  },
  methods: {
  fetchJokes() {
    axios.get(`https://icanhazdadjoke.com/search?term=${this.searchTerm}`, {
      headers: {
        'Accept': 'application/json'
      },
    })
    .then(response => {
      this.jokes = response.data.results;
      
    })
    .catch(error => {
      console.log(error);
    });
  },
  onInput() {
    clearTimeout(this.timeout);
    this.timeout = setTimeout(() => {
      this.fetchJokes();
    }, 500)
  }
},
mounted() {
  this.fetchJokes();
},
  components: {
    JokesComp
  },

}
</script>

<style scoped>
.center {
  display:grid;
  justify-content: center;
  margin-top:100px;
}
input {
  outline:none;
}
</style>
