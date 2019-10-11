<template>
  <div class="content">
    <div class="row">
      <div class="col-md-3"></div>
      <div class="col-md-3">
        <input
          type="text"
          class="form-control TextBox"
          placeholder="Search for..."
          v-model="searchString"
        />
      </div>
      <div class="col-md-1">
        <input type="submit" class="btn btn-primary" value="Search" v-on:click="handleSubmit" />
      </div>
      <div class="col-md-4">
        <div style="width:400px" class="alert alert-info" role="alert"><b>Example:</b> amygdala, insula, and the ventral</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "search-page",
  data() {
    return {
      searchString: ""
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("searchstring", this.searchString);
    }
  }
};
</script>

<style scoped>
.TextBox {
  width: 450px;
}
.content {
  padding-top: 20px;
  padding-bottom: 20px;
}
</style>