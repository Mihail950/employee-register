<template>
  <button
    :class="{ button_active: page == currentPage }"
    @click="goToPage(page)"
  >
    {{ page }}
  </button>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import router from "@/router";
export default {
  props: {
    page: {
      type: Number,
      requared: true,
    },
  },
  computed: {
    ...mapGetters({
      currentPage: "paginationModule/currentPage",
    }),
  },
  methods: {
    goToPage(page) {
      router.push("/page/" + page);
    },
  },
};
</script>
<style scoped>
button {
  background-color: #ffffff;
  border: 1px solid #e2e2e2;
  border-radius: 6px;
  color: #79838b;
  width: 30px;
  height: 30px;
  cursor: pointer;
}
.button_active {
  background-color: #e2e2e2;
  cursor: default;
}
</style>
