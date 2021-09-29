<template>
  <div :id="item.id" class="item">
      <img v-if="item.thumbnail" class="thumbnail" :alt="item.title" :src="item.thumbnail.url">
      <img v-else class="thumbnail" :alt="item.title" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAQAAAAAYLlVAAAAPElEQVR42u3OMQEAAAgDINfc5hpjDyQge1MVAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBgXbgAQzcYAEuE5tqAAAAAElFTkSuQmCC">
      <div class="infobox">
        <a :href="pageUrl" target="_blank">
          <div class="title">{{item.title}}</div>
        </a>
        <div class="description">{{item.description}}</div>
      </div>
  </div>
</template>

<script>
export default {
  name: "WikiSearchResponseItem",
  props: {
    item: Object,
    language: String,
  },
  data() {
    let uriEncodedPageKey = encodeURIComponent(this.item.key)
    return {
      pageUrl: `https://${this.language}.wikipedia.org/wiki/${uriEncodedPageKey}`
    }
  }
}
</script>

<style scoped>

a {
  text-decoration: none;
  color: #2c3e50;
}

.item {
  min-height: 4rem;
  padding: 10px;
  display: flex;
  align-items: flex-start;
  border-bottom: darkgray 1px solid;
}

.thumbnail {
  float: left;
  width: 64px;
  height: 64px;
  margin-right: 10px;
}

.infobox {
  flex: 1;
}

.title {
  font-weight: bolder;
  font-size: x-large;
}
</style>
