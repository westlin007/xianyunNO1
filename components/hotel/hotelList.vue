<template>
  <div class="hotel-lis">
    <el-row class="hotel-item" v-for="(item,index) in data" :key="index">
      <!-- 图片 -->
      <el-col :span="8">
        <a :href="`/hotel/detail?id=${item.id}`" class="img">
          <img
            :src="item.photos"/>
        </a>
      </el-col>

      <!-- 酒店信息 -->
      <el-col :span="10">
        <span class="hotel-name">
          <a :href="`/hotel/detail?id=${item.id}`">{{item.name}}</a>
        </span>
        <!-- 酒店等级 -->
        <el-row>
          <span>{{item.alias}}</span>
          <span>
            <i class="el-icon-star-on" 
            v-for="item1 in (item.hotellevel ? item.hotellevel.level : 0)" 
            :key="item1" 
            style="color:#f90"
            ></i>
          </span>
          <span>{{item.hoteltype.name}}</span>
        </el-row>

        <!-- 酒店评分 -->
        <el-row type="flex">
          <el-col :span="10">
            <el-rate
              v-model="item.stars"
              disabled
              show-score
              text-color="#ff9900"
              score-template="{value}分"
            ></el-rate>
          </el-col>
          <el-col :span="7">
            <span class="height-light">{{item.all_remarks}}</span>
            条评价
          </el-col>
          <el-col :span="7">
            <span class="height-light">12</span>
            篇游记
          </el-col>
        </el-row>

        <!-- 酒店位置 -->
        <div class="location">
          <i class="el-icon-location-information"></i>
          位于: {{item.address}}
        </div>
      </el-col>

      <!-- 平台价格 -->
      <el-col :span="6" class="price-col">
          <el-row 
          type="flex" 
          class="price-item" 
          align="middle" 
          justify="space-btween"
          v-for="(item2,index2) in item.products"
          :key=index2>
            <el-col >{{item2.name}}</el-col>
            <el-col >
              <span class="height-light">￥{{item2.price}}</span>起
              <i class="el-icon-arrow-right"></i>
            </el-col>
          </el-row>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  props:{
    data:{
      type:Array,
      default: ()=>[]
    }
  },
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