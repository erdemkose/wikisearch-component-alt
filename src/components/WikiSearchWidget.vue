<template>
  <div>

    <div v-if="loading">Loading...</div>

    <WikiSearchResponse v-if="!loading"
        :language="language"
        :footerMsg="`Search for pages containing ${query}`"
        :searchResponse="searchResponse"
    />
  </div>
</template>

<script>
import WikiSearchResponse from "@/components/WikiSearchResponse";
export default {
  name: "WikiSearchWidget",
  methods: {
    searchWiki() {
      this.loading = true

      fetch(this.endpoint)
          .then(async response => await response.json())
          .then(data => this.searchResponse = data.pages)

      this.loading = false
    }
  },
  props: {
    limit: String,
    query: String,
    language: String,
  },
  data() {
    let encodedQuery = encodeURIComponent(this.query)
    return {
      loading: false,
      searchResponse: [],
      endpoint: `https://${this.language}.wikipedia.org/w/rest.php/v1/search/title?q=${encodedQuery}&limit=${this.limit}`,
    }
  },
  mounted() {
    this.searchWiki()
  },
  components: {WikiSearchResponse}
}
</script>

<style scoped>

</style>
