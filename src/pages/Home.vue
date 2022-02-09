/* eslint-disable vue/no-unused-vars */
<template>
  <div class="text-center"><h2>Blog Posts</h2></div>
  <div class="q-pa-md row items-start q-gutter-md">
    <div v-for="(blogpost, index) in blogposts" :key="blogpost">
      <q-card class="my-card">
        <q-card-section class="bg-primary text-white">
          <div class="text-h6">{{ index + 1 }}.{{ blogpost.title }}</div>
          <div class="text-subtitle2">{{ blogpost.description }}</div>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right">
          <q-btn flat>View</q-btn>
        </q-card-actions>
      </q-card>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogposts: [],
    };
  },
  methods: {
    getAllPosts() {
      console.log("testing");
      this.$axios
        .get("http://localhost:3000/blogpost")
        .then(
          function (response) {
            console.log("res", response);
            this.blogposts = response.data;
            // Handle success
          }.bind(this)
        )
        .catch((e) => {
          console.log("error", e);
        });
    },
  },
  mounted() {
    this.getAllPosts();
  },
};
</script>
