<template>
  <div>
    <div class="filter">
      <el-row type="flex">
        <el-col class="filter-col" style="padding:5px 20px;">
          <el-row type="flex">
            <el-col>价格</el-col>
            <el-col>0-{{slider}}</el-col>
          </el-row>
          <el-slider v-model="slider" :max="4000" step="100"></el-slider>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>住宿等级</el-col>
          </el-row>
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>住宿类型</el-col>
          </el-row>
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>酒店设施</el-col>
          </el-row>
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>酒店品牌</el-col>
          </el-row>
          <el-select v-model="value" placeholder="请选择">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      slider: 4000
    };
  }
};
</script>
<style lang="less" scoped>
.filter {
  border: 1px solid #ddd;
  padding: 5px 0;
  .filter-col {
    border-right: 1px solid #ddd;
    &:last-child {
      border-right: 0;
    }
    .filter-title {
      padding: 0 15px;
    }
    /deep/.el-input__inner {
      border: none;
    }
  }
}
</style>