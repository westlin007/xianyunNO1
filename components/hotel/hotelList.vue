<template>
  <div class="hotel-lis">
    <el-row class="hotel-item">
      <!-- 图片 -->
      <el-col :span="8">
        <a href="#" class="img">
          <img
            src="http://qcloud.dpfile.com/pc/wQ2ejOSmhB4OoEq1LYPHp_2RhNciyW026YiQFr_EEZsQrI_ZB6abZPwgKDOmI03U3dWYFEM5hoslgWXTJDjSPA.jpg"
          />
        </a>
      </el-col>

      <!-- 酒店信息 -->
      <el-col :span="10">
        <span class="hotel-name">
          <a href="#">好来阁商务宾馆</a>
        </span>
        <!-- 酒店等级 -->
        <el-row>
          <span>hao lai ge shang wu hotel</span>
          <span>
            <i class="el-icon-star-on" v-for="item in 4" :key="item" style="color:#f90"></i>
          </span>
          <span>经济型</span>
        </el-row>

        <!-- 酒店评分 -->
        <el-row type="flex">
          <el-col :span="10">
            <el-rate
              v-model="value"
              disabled
              show-score
              text-color="#ff9900"
              score-template="{value}"
            ></el-rate>
          </el-col>
          <el-col :span="7">
            <span class="height-light">9</span>
            条评价
          </el-col>
          <el-col :span="7">
            <span class="height-light">79</span>
            篇游记
          </el-col>
        </el-row>

        <!-- 酒店位置 -->
        <div class="location">
          <i class="el-icon-location-information"></i>
          位于: 高淳县淳溪镇镇兴路118号(高淳县委党校对面)
        </div>
      </el-col>

      <!-- 平台价格 -->
      <el-col :span="6" class="price-col">
        <a href="#">
          <el-row type="flex" class="price-item" align="middle" justify="space-btween">
            <el-col >携程</el-col>
            <el-col >
              <span class="height-light">￥84</span>起
              <i class="el-icon-arrow-right"></i>
            </el-col>
          </el-row>
        </a>
        <a href="#">
          <el-row type="flex" class="price-item" align="middle" justify="space-btween">
            <el-col >艺龙</el-col>
            <el-col >
              <span class="height-light">￥84</span>起
              <i class="el-icon-arrow-right"></i>
            </el-col>
          </el-row>
        </a>
        <a href="#">
          <el-row type="flex" class="price-item" align="middle" justify="space-btween">
            <el-col>Hotel.com</el-col>
            <el-col >
              <span class="height-light">￥84</span>起
              <i class="el-icon-arrow-right"></i>
            </el-col>
          </el-row>
        </a>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: 3.7
    };
  }
};
</script>
<style lang="less" scoped>
.hotel-item {
  border-bottom: 1px solid #ddd;
  padding: 25px 0;
  .img {
    display: block;
    width: 320px;
    height: 210px;
    overflow: hidden;
    img {
      width: 100%;
    }
  }
  .hotel-name {
    font-weight: 400;
    font-size: 24px;
  }
  .location {
    padding-top: 10px;
  }
  .price-col {
    padding: 20px 10px 0;
    .price-item {
      padding-left: 20px;
      height: 44px;
      border-bottom: 1px solid #ddd;
    }
  }
}
.height-light {
  color: #f90;
}
</style>