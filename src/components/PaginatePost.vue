<script setup>
defineProps(['start', 'end']);
const emit = defineEmits(['next','before']);
</script>

<template>
  <div class="container">
    <div class="btn-group" role="group" aria-label="Basic example">
      <button type="button" class="btn btn-outline-primary" @click='emit("before")' :disabled='start<=0'>Previus {{start}}</button>
      <button type="button" class="btn btn-outline-primary" @click='emit("next")' :disabled='end>=100'>Next {{end}}</button>
    </div>
  </div>
</template>


<style lang="scss" scoped>
</style>