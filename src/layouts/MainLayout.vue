<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title> Dev Blog </q-toolbar-title>
        <q-btn
          style="background: goldenrod; color: white"
          @click="onClickAddPost()"
          label="Add New Post"
        />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <div class="text-center">Dev Blog</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    onClickAddPost() {
      this.$router.push("/create");
    },
  },
};
</script>