<template>
  <q-page>
    <q-circular-progress
      indeterminate
      size="75px"
      :thickness="0.2"
      color="blue-grey-6"
      class="q-ma-md fixed-center"
      v-if="isLoading"
    />
    <q-list separator padding>
      <q-item 
        clickable 
        v-ripple
        v-for="post in posts"
        :key="post.data.id"
        @click="onPostClick(post.data.preview.images[0].source.url)"
      >
        <q-item-section avatar>
          <q-avatar size="100px" rounded>
            <img :src="post.data.thumbnail">
          </q-avatar>
        </q-item-section>
        <q-item-section>{{ post.data.title }}</q-item-section>
      </q-item>
    </q-list>

    <q-dialog full-width v-model="showImageDialog">
      <q-card>
        <q-card-section class="row items-center justify-between">
          <q-space />
          <q-btn icon="close" flat round dense v-close-popup />
        </q-card-section>

        <q-card-section>
          <q-img 
            :src="imageUrl"
            spinner-color="teal"
            spinner-size="50px"
          />
        </q-card-section>
      </q-card>
    </q-dialog>

  </q-page>
</template>

<style></style>

<script>
export default {
  name: "PageIndex",
  data:() => ({
    posts: [],
    isLoading: false,
    imageUrl: '',
    showImageDialog: false,
  }),
  methods: {
    onPostClick(image) {
      this.showImageDialog = true;
      this.imageUrl = image;
    }
  },
  created() {
    this.isLoading = true;
    this.$axios.get("https://www.reddit.com/r/cats.json?raw_json=1")
      .then(res => {
        this.isLoading = false;
        this.posts = res.data.data.children;
      }).catch(err => {
        this.isLoading = false;
        console.log(err);
      })
  }
};
</script>
