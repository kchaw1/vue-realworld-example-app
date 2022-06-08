<template>
  <div>
    <div v-if="isLoading" class="article-preview">Loading history...</div>
    <div v-else>
      <div v-if="history.length === 0" class="article-preview">
        No history.
      </div>
      <RwvHistory
        v-for="(hist, index) in history"
        :history="hist"
        :key="hist.title + index"
      />
      <VPagination :pages="pages" :currentPage.sync="currentPage" />
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import RwvHistory from "./VHistory";
import VPagination from "./VPagination";
import { FETCH_HISTORY } from "../store/actions.type";

export default {
  name: "RwvHistoryList",
  components: {
    RwvHistory,
    VPagination
  },
  props: {
    type: {
      type: String,
      required: false,
      default: "all"
    },
    itemsPerPage: {
      type: Number,
      required: false,
      default: 10
    }
  },
  data() {
    return {
      currentPage: 1
    };
  },
  computed: {
    listConfig() {
      const { type } = this;
      const filters = {
        offset: (this.currentPage - 1) * this.itemsPerPage,
        limit: this.itemsPerPage
      };
      return {
        type,
        filters
      };
    },
    pages() {
      if (this.isLoading || this.historyCount <= this.itemsPerPage) {
        return [];
      }
      return [
        ...Array(Math.ceil(this.historyCount / this.itemsPerPage)).keys()
      ].map(e => e + 1);
    },
    ...mapGetters(["historyCount", "isLoading", "history"])
  },
  watch: {
    currentPage(newValue) {
      this.listConfig.filters.offset = (newValue - 1) * this.itemsPerPage;
      this.fetchHistory();
    },
    type() {
      this.resetPagination();
      this.fetchHistory();
    }
  },
  mounted() {
    this.fetchHistory();
  },
  methods: {
    fetchHistory() {
      this.$store.dispatch(FETCH_HISTORY, this.listConfig);
    },
    resetPagination() {
      this.listConfig.offset = 0;
      this.currentPage = 1;
    }
  }
};
</script>
