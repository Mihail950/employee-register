<template>
  <div class="page">
    <div class="button-box">
      <div class="back-button" @click="GoBack">
        <img
          width="18px"
          height="18px"
          src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAAA2UlEQVR4nO3ZTarCYAyF4azQq3LFge7DZJp0YtI9CgoquAQF5cOBIDo2+TgPdN7D20J/iAD6tRl8JhYnMb+Ixj9VxLZdssVVLO7Pwy9Uf0TcWf1M5UdYXEVjTlXw4Iv3EaJ+YxtXVAVGZIESWaBEFiiRBUpkwXjsSIJRIgnuoYToOP30UtRelqgSsTiUH9HXEO3k0mra96dPN7uor6kawZikBGWSEpRJSlAmKZTJCmWyQpmsuirDX36Gbgb/o05+T++povcxrH6kqtrlJBa7VoN1nPz6fADo5QGWDa1BKTabyAAAAABJRU5ErkJggg=="
          alt="back"
        />Назад
      </div>
    </div>
    <div class="card">
      <div class="img-block">
        <img
          class="avatar"
          width="370px"
          v-if="this.currentEmployee.photo"
          :src="'data:image/jpeg;base64,' + this.currentEmployee.photo"
        />
        <img
          class="avatar"
          width="370px"
          height="370px"
          v-if="!this.currentEmployee.photo"
          src="\src\assets\avatar.png"
        />
      </div>
      <div class="profile-info">
        <h2 class="profile-name">
          {{ this.currentEmployee.lastName }} <br />
          {{ this.currentEmployee.firstName }}<br />
          {{ this.currentEmployee.middleName }}<br />
        </h2>
        <h4>Департамент:</h4>
        <p>{{ this.currentEmployee.department }}</p>
        <h4>Должность:</h4>
        <p>{{ this.currentEmployee.post }}</p>
        <h4>Дата рождения:</h4>

        <p>
          {{ this.currentEmployee.birthDate.split("T")[0].split("-")[0] }}.{{
            this.currentEmployee.birthDate.split("T")[0].split("-")[1]
          }}.{{ this.currentEmployee.birthDate.split("T")[0].split("-")[2] }}
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters({
      currentEmployee: "employeesModule/currentEmployee",
    }),
  },
  methods: {
    GoBack() {
      this.$router.push("/");
    },
  },
};
</script>
<style scoped>
h4 {
  color: #b8c5d0;
  font-size: 11px;
}
.page {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 15px;
}
.button-box {
  width: 800px;
  margin: 130px 0 10px 10px;
}
.card {
  width: 800px;
  height: 400px;
  background-color: #fff;
  display: flex;
  border-radius: 38px;
}
.avatar {
  border-radius: 30px;
}
.back-button {
  width: 80px;
  padding: 0;
  font-weight: 600;
  font-size: 20px;
  cursor: pointer;
  transition: transform 0.2s;
  display: flex;
  align-items: center;
  gap: 10px;
}
.back-button:hover {
  transform: translateY(-4px);
}
.profile-info {
  margin: 25px auto 0 40px;
  text-align: left;
}
.profile-name {
  font-size: 40px;
}
.img-block {
  width: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
