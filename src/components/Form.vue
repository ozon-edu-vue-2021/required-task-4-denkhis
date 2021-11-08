<template>
  <el-container>
    <div class="form">
      <form action="">
        <personal-data v-model="personalData" />
        <passport-data v-model="passportData" />
        <el-button type="primary" @click.native="handleSubmit">
          Отправить
        </el-button>
      </form>
    </div>
  </el-container>
</template>

<script>
import PersonalData from "./PersonalData.vue";
import PassportData from "./PassportData.vue";
export default {
  components: {
    PersonalData,
    PassportData,
  },
  data() {
    return {
      personalData: {
        firstName: "",
        secondName: "",
        lastName: "",
        birthDate: "",
        email: "",
        gender: "",
      },
      passportData: {
        citizenship: null,
        passportSeries: "",
        passportNumber: "",
        issueDate: "",
        issueCountry: "",
        passportType: "",
        firstNameLatin: "",
        secondNameLatin: "",
        isNameChanged: false,
        previousFirstName: "",
        previousLastName: "",
      },
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
