<script setup>
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "description none",
  },
  changeFav: Function,
  deletePost: Function,
});
</script>

<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ id }} - {{ title }}</h5>
        <p>{{ body }}</p>
        <button @click="changeFav(title)" class="btn btn-outline-primary">
          Favorite
        </button>
        <button @click='deletePost(id)' class="btn btn-outline-danger">Delete</button>
      </div>
    </div>
  </div>
</template>

