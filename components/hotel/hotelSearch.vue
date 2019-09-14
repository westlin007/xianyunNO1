<template>
  <div>
    <el-form :inline="true" ref="form" :model="form">
      <!-- 城市 -->
      <el-form-item>
        <el-input 
        v-model="form.city" 
        placeholder="城市"
        ></el-input>
      </el-form-item>
      
      <!-- 日期 -->
      <el-form-item required>
        <el-col :span="10">
          <el-date-picker
            type="daterange"
            range-separator="-"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            v-model="form.date"
          ></el-date-picker>
        </el-col>
      </el-form-item>

      <!-- 人数 -->
      <el-form-item>
        <el-input 
        placeholder="人数未定" 
        suffix-icon="el-icon-user" 
        v-model="form.num"
        ></el-input>
      </el-form-item>

      <!-- 按钮 -->
      <el-form-item>
        <el-button type="primary" @click="onSubmit">查看价格</el-button>
      </el-form-item>
      
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        city: "",
        date: "",
        num: "",
      }
    };
  },
  methods: {
    onSubmit() {
      console.log("submit!");
    }
  }
};
</script>