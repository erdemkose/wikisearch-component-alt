<template>
  <div class="pages">
    <div v-for="responseItem in searchResponse" v-bind:key="responseItem.id">
      <WikiSearchResponseItem
          :item="responseItem"
          :language="language"
      />
    </div>
    <div class="footer">
      {{footerMsg}}
    </div>
  </div>
</template>

<script>
import WikiSearchResponseItem from "@/components/WikiSearchResponseItem";
export default {
  name: "WikiSearchResponse",
  components: {WikiSearchResponseItem},
  props: {
    searchResponse: Array,
    footerMsg: String,
    language: String,
  },
  data() {
    return {
      responseItem: null,
    }
  }
}
</script>

<style scoped>

.pages {
  border: darkgray 1px solid;
}

.footer {
  padding: 10px;
}
</style>
