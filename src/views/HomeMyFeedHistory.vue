<template>
  <div class="home-my-feed-history"><RwvHistoryList type="all" /></div>
</template>

<script>
import RwvHistoryList from "@/components/HistoryList";

export default {
  name: "rwv-home-my-feed-history",
  components: {
    RwvHistoryList
  }
};
</script>
