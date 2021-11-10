<template>
  <el-row :gutter="20">
    <el-col>
      <h2>Паспортные данные</h2>
    </el-col>

    <el-col :span="12" class="select">
      <input
        v-model="searchString"
        v-click-outside="hideDropdown"
        placeholder="Гражданство"
        class="input"
        @focus="isDropdownOpen = true"
      />
      <div v-if="isDropdownOpen" class="select-dropdown">
        <ul v-if="citizenships.length">
          <li
            v-for="item in filteredCitizenships"
            :key="item.id"
            @click="selectCountry(item.nationality)"
          >
            {{ item.nationality }}
          </li>
        </ul>
        <div v-else>Пусто</div>
      </div>
    </el-col>

    <template v-if="value.citizenship">
      <template v-if="value.citizenship === russianNationality">
        <el-col :span="8">
          <el-input
            v-model="value.passportSeries"
            placeholder="Серия паспорта"
          />
        </el-col>
        <el-col :span="8">
          <el-input
            v-model="value.passportNumber"
            placeholder="Номер паспорта"
          />
        </el-col>
        <el-col :span="8">
          <el-date-picker
            v-model="value.issueDate"
            type="date"
            placeholder="Дата выдачи"
          />
        </el-col>
      </template>
      <template v-else>
        <el-col :span="10">
          <el-input
            v-model="value.secondNameLatin"
            placeholder="Фамилия на латинице"
          />
        </el-col>
        <el-col :span="10">
          <el-input
            v-model="value.firstNameLatin"
            placeholder="Имя на латинице"
          />
        </el-col>
        <el-col :span="8">
          <el-input
            v-model="value.passportNumber"
            placeholder="Номер паспорта"
          />
        </el-col>
        <el-col :span="8">
          <el-select v-model="value.issueCountry" placeholder="Страна выдачи">
            <el-option
              v-for="item in citizenships"
              :key="item.id"
              :label="item.nationality"
              :value="item.id"
            >
            </el-option>
          </el-select>
        </el-col>
        <el-col :span="8">
          <el-select v-model="value.passportType" placeholder="Тип паспорта">
            <el-option
              v-for="item in passportTypes"
              :key="item.id"
              :label="item.type"
              :value="item.id"
            >
            </el-option>
          </el-select>
        </el-col>
      </template>
    </template>
    <el-col>
      <h4>Меняли фамилию или имя?</h4>
      <el-radio-group v-model="value.isNameChanged">
        <el-radio :label="true">Да</el-radio>
        <el-radio :label="false">Нет</el-radio>
      </el-radio-group>
    </el-col>
    <template v-if="value.isNameChanged">
      <el-col :span="8">
        <el-input v-model="value.previousLastName" placeholder="Фамилия" />
      </el-col>
      <el-col :span="8">
        <el-input v-model="value.previousFirstName" placeholder="Имя" />
      </el-col>
    </template>
  </el-row>
</template>

<script>
import citizenships from "../assets/data/citizenships.json";
import passportTypes from "../assets/data/passport-types.json";
import ClickOutside from "vue-click-outside";

export default {
  // watch: {
  //   searchString: {
  //     handler(nV) {
  //       console.log(nV);
  //     },
  //   },
  // },
  directives: {
    ClickOutside,
  },
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      searchString: "",
      isDropdownOpen: false,
      citizenships,
      passportTypes,
    };
  },
  computed: {
    russianNationality() {
      return "Russia";
    },
    filteredCitizenships() {
      return this.citizenships.filter((item) => {
        return item.nationality
          .toLowerCase()
          .includes(this.searchString.toLowerCase());
      });

      // return this.allSkills.reduce((acc, curr) => {
      //   if (!this.isSkillAlreadyExist(curr)) {
      //     acc.push(curr);
      //   }
      //   return acc;
      // }, []);
    },
  },
  methods: {
    hideDropdown() {
      this.isDropdownOpen = false;
    },
    selectCountry(citizenship) {
      this.$emit("set-citizenship", citizenship);
    },
  },
};
</script>
