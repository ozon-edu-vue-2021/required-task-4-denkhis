<template>
  <el-row :gutter="20">
    <el-col>
      <h2>Личные данные</h2>
    </el-col>
    <el-col :span="8">
      <el-input placeholder="Фамилия" />
    </el-col>
    <el-col :span="8">
      <el-input placeholder="Имя" />
    </el-col>
    <el-col :span="8">
      <el-input placeholder="Отчество" />
    </el-col>
    <el-col :span="24">
      <el-date-picker
        v-model="value1"
        type="date"
        placeholder="Дата рождения"
      />
    </el-col>
    <el-col :span="12">
      <el-input placeholder="Email" />
    </el-col>
    <el-col class="mb20">
      <h4>Пол</h4>
      <el-radio-group v-model="radio">
        <el-radio :label="3">Мужской</el-radio>
        <el-radio :label="6">Женский</el-radio>
      </el-radio-group>
    </el-col>
  </el-row>
</template>

<script>
export default {};
</script>
