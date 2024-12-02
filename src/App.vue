<script>
import { mapActions, mapGetters } from "vuex";
export default {
  methods: {
    ...mapActions({
      searchEmployee: "employeesModule/searchEmployee",
      setPageQuantity: "paginationModule/setPageQuantity",
      setPagesArr: "paginationModule/setPagesArr",
    }),
  },
  mounted() {
    this.searchEmployee({ name: "" });
    this.setPageQuantity();
    this.setPagesArr();
  },
};
</script>

<template>
  <RouterView />
</template>

<style scoped></style>
