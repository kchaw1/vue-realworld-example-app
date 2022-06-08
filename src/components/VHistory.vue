<template>
  <div class="article-preview">
    <h1 v-text="history.title" />
    <p v-text="history.description" />
  </div>
</template>

<script>
export default {
  name: "RwvHistory",
  props: {
    history: { type: Object, required: true }
  }
};
</script>
