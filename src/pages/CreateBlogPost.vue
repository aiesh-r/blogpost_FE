<template>
  <div class="title-bar text-center"><h2>Create New Post</h2></div>
  <div class="q-pa-md">
    <q-form @submit="onSubmit" @reset="onReset" class="create-post-form">
      <q-input
        filled
        v-model="title"
        label="Blogpost Title *"
        hint="Name"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || 'Please type something']"
      />

      <q-input
        filled
        v-model="description"
        label="Description"
        lazy-rules
        :rules="[
          (val) =>
            (val.length !== 0 && val !== '') ||
            'Please type text about the post',
        ]"
      />

      <div>
        <q-btn label="Create Post" type="submit" color="primary" />
        <q-btn
          label="Reset"
          type="reset"
          color="primary"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { ref } from "vue";
import { axios } from "boot/axios";
export default {
  data() {
    return {
      submitDone: "",
      title: "",
      description: "",
    };
  },
  setup() {
    const $q = useQuasar();
    const title = ref(null);
    const description = ref(null);

    return {
      //   this.title,
      //   this.description,
      onSubmit() {
        axios
          .post("http://localhost:3000/blogpost", {
            title: title,
            description: description,
          })
          .then((response) => {
            console.log("response of post", response);
            this.submitDone = response.data;
            $q.notify({
              color: "green-4",
              textColor: "white",
              icon: "cloud_done",
              message: "Blogpost created successfully",
            });
          })
          .catch((e) => {
            console.log("error occured in create post", e);
            $q.notify({
              color: "$negative",
              textColor: "white",
              icon: "cloud_done",
              message: "Blogpost creation failed",
            });
          });
      },
      onReset() {},
    };
  },
};
</script>

<style scoped>
.create-post-form {
  position: fixed;
  top: auto;
  left: 50%;
  max-width: 1000px;
  justify-items: start;
}
</style>