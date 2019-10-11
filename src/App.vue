<template>
  <div id="app">
    <search-page @searchstring="getkeywords" />
    <search-result :searchString="searchString" />
  </div>
</template>

<script>
import SearchPage from "./components/SearchPage.vue";
import SearchResult from "./components/SearchResult.vue";

export default {
  name: "app",
  components: {
    SearchPage,
    SearchResult
  },
  data() {
    return {
      searchString: ""
    };
  },
  methods: {
    getkeywords(keywords) {
      this.searchString = keywords;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
