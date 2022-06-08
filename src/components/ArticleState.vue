<template>
  <div>
    <div :style="styleObject" :class="toggleState">{{ type }}</div>
  </div>
</template>

<script>
export default {
  name: "ArticleState",
  props: {
    type: {
      type: String,
      required: true
    }
  },
  data: function() {
    return {
      styleObject: {
        width: "80px",
        height: "30px"
      }
    };
  },
  computed: {
    toggleState() {
      if (this.type === "CREATE") {
        return "state-create";
      } else if (this.type === "UPDATE") {
        return "state-update";
      } else {
        return "state-delete";
      }
    }
  }
};
</script>
