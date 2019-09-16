<template>
  <div>
    <div class="filter">
      <el-row type="flex">
        <el-col class="filter-col" style="padding:5px 20px;">
          <el-row type="flex">
            <el-col>价格</el-col>
            <el-col>0-{{slider}}</el-col>
          </el-row>
          <el-slider v-model="slider" :max="4000" :step="100"></el-slider>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>住宿等级</el-col>
          </el-row>
          <el-select
            v-model="ranksValue"
            clearable
            @clear="handleRankEmpty"
            collapse-tags
            placeholder="不限"
            @change="handleRank"
          >
            <el-option
              v-for="(item,index) in ranks"
              :key="index"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>住宿类型</el-col>
          </el-row>
          <el-select
            v-model="typesValue"
            clearable
            @clear="handleTypesEmpty"
            collapse-tags
            @change="handleTypes"
            placeholder="不限"
          >
            <el-option
              v-for="(item,index) in types"
              :key="index"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>酒店设施</el-col>
          </el-row>
          <el-select
            v-model="facilityValue"
            clearable
            @clear="handleFacilitysEmpty"
            collapse-tags
            @change="handleFacilitys"
            placeholder="不限"
          >
            <el-option
              v-for="(item,index) in facilitys"
              :key="index"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-col>
        <el-col class="filter-col">
          <el-row type="flex" class="filter-title">
            <el-col>酒店品牌</el-col>
          </el-row>
          <el-select
            v-model="brandValue"
            clearable
            @clear="handleBrandsEmpty"
            collapse-tags
            @change="handleBrands"
            placeholder="不限"
          >
            <el-option
              v-for="(item,index) in brands"
              :key="index"
              :label="item.name"
              :value="item.id"
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
      slider: 4000,
      options: [],
      value: "",
      //住宿等级
      ranks: [],
      //住宿类型
      types: [],
      // 设施
      facilitys: [],
      //酒店品牌
      brands: [],
      // 绑定数据
      ranksValue: [],
      typesValue: [],
      facilityValue: [],
      brandValue: [],

      hotelasset: 0,
      hotelbrand: 0, 
      hoteltype: 0, 
      hotellevel: 0, 
      price_in: 0 
    };
  },
  methods: {
    //价格筛选
    handleSlider(value) {
      // console.log(value);
      this.$emit("setDataList", { price_lt: value });
    },
    //住宿等级
    handleRank(value) {
      // console.log(value);

      this.$emit("setDataList", { hotellevel: value });
    },
    //清空住宿等级
    handleRankEmpty(value) {
      this.$emit("setDataList", {});
    },
    //住宿类型
    handleTypes(value) {
      // console.log(value);
      this.$emit("setDataList", { hoteltype: value });
    },
    //清空住宿类型
    handleTypesEmpty() {
      this.$emit("setDataList", {});
    },
    //设施
    handleFacilitys(value) {
      // console.log(value);

      this.$emit("setDataList", { hotelasset: value });
    },
    //清空设施
    handleFacilitysEmpty() {
      this.$emit("setDataList", {});
    },
    //酒店品牌
    handleBrands(value) {
      // console.log(value);
      this.$emit("setDataList", { hotelbrand: value });
    },
    //清空品牌
    handleBrandsEmpty() {
      this.$emit("setDataList", {});
    }
  },
  mounted() {
    //获取酒店筛选条件
    this.$axios({
      url: "/hotels/options"
    }).then(res => {
      const { data } = res.data;
      // console.log(data)
      if (res.status == 200) {
        this.ranks = data.levels;
        this.types = data.types;
        this.facilitys = data.assets;
        this.brands = data.brands;
      }
    });
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