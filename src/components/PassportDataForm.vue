<template>
  <el-row :gutter="20">
    <el-col>
      <h2>Паспортные данные</h2>
    </el-col>
    <!-- <el-col :span="20">
      <el-select v-model="value.citizenship" placeholder="Гражданство">
        <el-option
          v-for="item in citizenships"
          :key="item.id"
          :label="item.nationality"
          :value="item.id"
        >
        </el-option>
      </el-select>
    </el-col> -->

    <el-col :span="12" class="select">
      <el-input v-model="value.citizenship" placeholder="Гражданство" />
      <div v-if="true" class="select-dropdown">
        <ul>
          <li v-for="index in 10" :key="index">item {{ index }}</li>
        </ul>
      </div>
    </el-col>

    <template v-if="value.citizenship">
      <template v-if="value.citizenship === russianId">
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

export default {
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      citizenships,
      passportTypes,
    };
  },
  computed: {
    russianId() {
      return this.citizenships.find((item) => item.nationality === "Russia").id;
    },
  },
};
</script>

<style scoped>
.select {
  display: flex;
  flex-direction: column;
  position: relative;
}

.select-dropdown {
  border-radius: 5px;
  box-shadow: 1px 1px 5px grey;
  background-color: white;
  width: 100%;
  position: absolute;
  top: 50px;
  z-index: 1;
  cursor: pointer;
}

.select-dropdown ul {
  padding: 0;
}

.select-dropdown li {
  list-style: none;
  padding-left: 10px;
  border-radius: 5px;
  user-select: none;
}

.select-dropdown li:hover {
  background: lightskyblue;
  list-style: none;
}
</style>
