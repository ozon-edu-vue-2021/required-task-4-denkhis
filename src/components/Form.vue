<template>
  <el-container>
    <div class="form">
      <form action="">
        <personal-data-form v-model="personalData" />
        <passport-data-form
          v-model="passportData"
          :citizenship-type="citizenshipType"
          @set-citizenship="setCitizenship"
        />
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
import { omitBy, isNull } from "lodash";

export default {
  components: {
    PersonalDataForm,
    PassportDataForm,
  },
  watch: {
    "passportData.citizenship": {
      handler(newVal) {
        this.citizenshipType = newVal === "Russia" ? 1 : 2;
      },
    },
    "passportData.isNameChanged": {
      handler() {
        this.passportData.previousFirstName = null;
        this.passportData.previousLastName = null;
      },
    },
    citizenshipType() {
      this.passportData.passportSeries = null;
      this.passportData.passportNumber = null;
      this.passportData.issueDate = null;
      this.passportData.issueCountry = null;
      this.passportData.passportType = null;
      this.passportData.firstNameLatin = null;
      this.passportData.secondNameLatin = null;
    },
  },
  data() {
    return {
      citizenshipType: null,
      personalData,
      passportData,
    };
  },
  methods: {
    setCitizenship(citizenship) {
      this.passportData.citizenship = citizenship;
    },
    handleSubmit() {
      console.log(
        omitBy(this.personalData, isNull),
        omitBy(this.passportData, isNull)
      );
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 600px;
}
</style>
