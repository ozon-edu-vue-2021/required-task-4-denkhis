<template>
  <el-container>
    <div class="form">
      <form action="">
        <personal-data />
        <passport-data />
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
        citizenship: "",
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
};
</script>
