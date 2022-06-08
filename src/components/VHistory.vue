<template>
  <div class="article-preview">
    <div class="article-meta">
      <div class="info">
        <span class="date">
          {{ history.occurredAt.replace("T", " ") }}
        </span>
      </div>
      <button
        class="btn btn-sm pull-sm-right"
        :class="{
          'btn-primary': history.type === 'CREATE',
          'btn-info': history.type === 'UPDATE',
          'btn-second': history.type === 'DELETE'
        }"
        v-text="history.type"
      />
    </div>
    <h2 v-text="history.title" />
    <div v-text="history.description" />
    <div
      v-text="history.body"
      :title="history.body"
      style="font-size: 0.8rem; overflow: hidden; text-overflow: ellipsis; white-space:now-rap;"
    />
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
