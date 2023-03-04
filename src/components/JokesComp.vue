<template>
  <div class="jokes">
 <router-link :to="`/about/${joke.id}`"><p>{{ joke.joke }}</p></router-link>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    joke: {
      required:true,
    }
  }
}
</script>

<style scoped>
.jokes {
  width:auto;
  padding: 1rem;
  border: 1px dotted #ccc;
  margin: 1rem 0;
}
</style>
