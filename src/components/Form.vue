<template>
  <el-container>
    <div class="form">
      <form action="">
        <personal-data-form v-model="personalData" />
        <passport-data-form v-model="passportData" />
        <el-button type="primary" @click.native="handleSubmit">
          Отправить
        </el-button>
      </form>
    </div>
  </el-container>
</template>

<script>
import PersonalDataForm from "./PersonalDataForm.vue";
import PassportDataForm from "./PassportDataForm.vue";
import { personalData, passportData } from "../assets/data/data";

export default {
  components: {
    PersonalDataForm,
    PassportDataForm,
  },
  watch: {
    "passportData.citizenship": {
      handler() {
        this.passportData.passportSeries = "";
        this.passportData.passportNumber = "";
        this.passportData.issueDate = "";
      },
    },
  },
  data() {
    return {
      personalData,
      passportData,
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.personalData, this.passportData);
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 600px;
}
</style>
