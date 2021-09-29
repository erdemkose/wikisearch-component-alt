<template>
  <div id="app">
    <form @submit.prevent="updateSearchKey()">
      <input v-model="query" class="query" type="text">
      <select v-model="language" class="language">
        <option value="en" selected>English</option>
        <option value="de">Deutsch</option>
        <option value="tr">Türkçe</option>
      </select>
      <select v-model="limit" class="limit">
        <option value="5">5</option>
        <option value="10" selected>10</option>
        <option value="20">20</option>
      </select>
      <button>Search Wiki</button>
    </form>

    <div v-if="!searchKey">Search for something first</div>

    <WikiSearchWidget v-if="searchKey"
        :key="searchKey"
        :limit="limit"
        :query="query"
        :language="language"
    />
  </div>
</template>

<script>
import WikiSearchWidget from "@/components/WikiSearchWidget";

export default {
  name: 'App',
  components: {
    WikiSearchWidget
  },
  data() {
    return {
      limit: 10,
      query: "",
      language: "en",
      searchKey: "",
    }
  },
  methods: {
    updateSearchKey() {
      this.searchKey = `${this.language}|${this.limit}|${this.query}`
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.query, .language, .limit {
  margin: 5px;
}
</style>
