<template>
  <el-row type="flex" class="row-bg" justify="center">
    <el-col :xs="24" :sm="18" :md="16" :lg="14" :xl="12">
      <h2>{{title}}</h2>
      <div v-html="content" class="markdown-body" v-highlight></div>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: "ArticleDetail",
  props: ["alias"],
  data() {
    return {
      content: "",
      title: ""
    };
  },

  created() {
    this.$http
      .get("/api/articleDetail", {
        params: {
          alias: this.alias
        }
      })
      .then(result => {
        this.content = result.data.Content;
        this.title = result.data.Title;
      });
  }
};
</script>

<style scoped>
@import url("../../assets/github-markdown.css");

h2 {
  margin: 30px auto;
  text-align: center
}

.row-bg {
  padding: 70px 20px 20px;
  background-color: #ffffff;
  min-height: 100%;
}
</style>
