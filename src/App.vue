<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";
const posts = ref([]);
const postXpage = 4;
const start = ref(0);
const end = ref(postXpage);
const loading = ref(true);

const fav = ref("");

const changeFav = (title) => {
  fav.value = title;
};


const next = () => {
  start.value = start.value + postXpage;
  end.value = end.value + postXpage;
};

const before = () => {
  if (start.value === 0) {
    return 0;
  } else {
    start.value = start.value - postXpage;
    end.value = end.value - postXpage;
  }
};

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value= false;
    }, 1000);
  }
});


const deletePost = (id) => {
  posts.value = posts.value.filter(post => post.id !== id);
};
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>App Vue.js</h1>
    <h2>My favorite post: {{ fav }}</h2>
    <PaginatePost
      class="mb-2"
      @next="next"
      @before="before"
      @deletePost='deletePost'
      :start="start"
      :end="end"
    />
    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      :changeFav="changeFav"
       :deletePost="deletePost"
      class="mb-2"
    ></BlogPost>
  </div>
</template>

<style>
h1{
  color:rgb(0, 98, 255);
}
</style>