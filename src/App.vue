<script setup>
import gql from 'graphql-tag'
import { useQuery } from '@vue/apollo-composable'

const CHARACTERS_QUERY = gql`
  query Characters {
    characters {
      results {
        id
        name
        image
      }
    }
  }
`
const { result, loading, error } = useQuery(CHARACTERS_QUERY);

console.log(result.value, "result", error.value, loading.value)
</script>

<template>
  <p v-if="error">Error...</p>
  <p v-if="loading">Loading...</p>
  <!-- <p v-else v-for="character in result.characters.results" :key="character.id">
    {{ character.name }}
  </p> -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
