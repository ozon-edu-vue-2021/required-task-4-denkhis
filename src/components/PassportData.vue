<template>
  <el-row :gutter="20">
    <el-col>
      <h2>Паспортные данные</h2>
    </el-col>
    <el-col :span="20">
      <el-select v-model="value" placeholder="Гражданство">
        <el-option
          v-for="item in citizenships"
          :key="item.id"
          :label="item.nationality"
          :value="item.id"
        >
        </el-option>
      </el-select>
    </el-col>
    <template v-if="true">
      <el-col :span="8">
        <el-input placeholder="Серия паспорта" />
      </el-col>
      <el-col :span="8">
        <el-input placeholder="Номер паспорта" />
      </el-col>
      <el-col :span="8">
        <el-date-picker
          v-model="value1"
          type="date"
          placeholder="Дата выдачи"
        />
      </el-col>
    </template>
    <div v-else>456</div>
  </el-row>
</template>

<script>
import citizenships from "../assets/data/citizenships.json";
export default {
  data() {
    return {
      citizenships,
    };
  },
};
</script>
