<template>
  <the-pagination />
  <div class="page">
    <div>
      <input
        placeholder="Поиск"
        class="search"
        @keyup="goSearchEmployee"
        v-model="searchEmployeeValue"
      />
    </div>
    <employees-item v-for="employee in employeesVisible" :employee="employee" />
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import EmployeesItem from "../EmployeesItem.vue";
import ThePagination from "../ThePagination.vue";
import router from "@/router";
export default {
  components: { EmployeesItem, ThePagination },
  data() {
    return {
      searchEmployeeValue: "",
      employeesVisible: [],
    };
  },
  computed: {
    ...mapGetters({
      employeesGetter: "employeesModule/employeesVisible",
      currentPage: "paginationModule/currentPage",
    }),
  },
  watch: {
    employeesGetter: function (arr) {
      const arr1 = arr.slice(this.currentPage * 10 - 10, this.currentPage * 10);
      this.employeesVisible = arr1;
    },
    $route(to, from) {
      this.setCurrentPage({ pageNum: to.params.pageNum });
      this.setEmployeesVisiable();
    },
  },
  methods: {
    ...mapActions({
      searchEmployee: "employeesModule/searchEmployee",
      setCurrentPage: "paginationModule/setCurrentPage",
      setPagesArr: "paginationModule/setPagesArr",
    }),
    goSearchEmployee() {
      router.push("/page/1");
      this.searchEmployee({ name: this.searchEmployeeValue.toLowerCase() });
      this.setPagesArr();
    },
    setEmployeesVisiable() {
      const arr1 = this.employeesGetter.slice(
        this.currentPage * 10 - 10,
        this.currentPage * 10
      );
      this.employeesVisible = arr1;
    },
  },
  created() {
    this.goSearchEmployee();
  },
};
</script>
<style scoped>
.page {
  margin-top: 5px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5px;
}
.search {
  border: 1px solid #e2e2e2;
  height: 40px;
  width: 500px;
  font-size: 16px;
  border-radius: 5px;
  padding-left: 15px;
  font-family: "Roboto";
  font-weight: 500;
}
</style>
