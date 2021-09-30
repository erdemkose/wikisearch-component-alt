<template>
  <div>
    <div v-if="loading">Loading...</div>

    <WikiSearchPageList v-if="!loading"
      :pages="pages"
      :language="language"
      :footerMsg="`Search for pages containing ${query}`"
    />
  </div>
</template>

<script>
import WikiSearchPageList from "@/components/WikiSearchPageList";

export default {
  name: "WikiSearchWidget",
  methods: {
    searchWiki() {
      this.loading = true

      fetch(this.endpoint)
          .then(response => response.json())
          .then(data => this.pages = data.pages)
          .catch(error => {
            this.pages = []
            console.error('Error:', error);
          })

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
      pages: [],
      endpoint: `https://${this.language}.wikipedia.org/w/rest.php/v1/search/title?q=${encodedQuery}&limit=${this.limit}`,
    }
  },
  mounted() {
    this.searchWiki()
  },
  components: {
    WikiSearchPageList,
  },
}
</script>
