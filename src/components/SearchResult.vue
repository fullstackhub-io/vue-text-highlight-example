<template>
  <div v-if="searchString != ''" class="maincontent">
    <div class="row" style="padding-bottom:10px">
      <div class="col-md-2"></div>
      <div class="col-md-8" style="text-align:left">
        <b>Keywords:</b> &nbsp;
        <span
          v-for="item of stringToCSV()"
          :key="item.title"
          class="keywords badge badge-pill badge-info"
        >{{item}}</span>
      </div>
      <div class="col-md-2"></div>
    </div>
    <div class="row">
      <div class="col-md-2"></div>
      <div class="card col-md-8">
        <div class="container">
          <h4>
            <b>
              Title:
              <text-highlight :queries="stringToCSV()">{{posts.title}}</text-highlight>
            </b>
          </h4>
          <p>
            <span class="abstractText">Abstract:</span>
            <br />
            <text-highlight :queries="stringToCSV()">{{posts.abstract}}</text-highlight>
          </p>
        </div>
      </div>
      <div class="col-md-2"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue from "vue";
import TextHighlight from "vue-text-highlight";

Vue.component("text-highlight", TextHighlight);

export default {
  name: "search-result",
  props: {
    searchString: String
  },
  data() {
    return {
      posts: [],
      errors: []
    };
  },
  methods: {
    stringToCSV() {
      var stopWords = [
        "a",
        "an",
        "and",
        "are",
        "as",
        "at",
        "be",
        "but",
        "by",
        "for",
        "if",
        "in",
        "into",
        "is",
        "it",
        "no",
        "not",
        "of",
        "on",
        "or",
        "such",
        "that",
        "the",
        "their",
        "then",
        "there",
        "these",
        "they",
        "this",
        "to",
        "was",
        "will",
        "with"
      ];

      this.searchString = this.searchString.replace(",", " ");
      var inputKeywords = this.searchString.split(" ");
      var finalKeywords = inputKeywords.filter(el => !stopWords.includes(el));
      return finalKeywords;
    }
  },
  created() {
    axios
      .get(
        `https://api.federalreporter.nih.gov/v1/Projects/search?query=orgName%3ABOSTON%20UNIVERSITY&limit=1`
      )
      .then(response => {
        this.posts = response.data.items[0];
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<style scoped>
.abstractText {
  font-size: 14pt;
  font-weight: bold;
}
.maincontent {
  padding-top: 20px;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

.container {
  padding: 2px 16px;
  width: 90%;
}
.keywords {
  font-size: 12pt;
  height: 30px;
  padding-top: 6px;
  margin-right: 5px;
}
</style>