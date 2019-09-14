<template>
  <div class="container">

    <!-- 面包屑 -->
    <div class="breadcrumb">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">酒店</el-breadcrumb-item>
        <el-breadcrumb-item>南京酒店预定</el-breadcrumb-item>
      </el-breadcrumb>
    </div>

    <!-- 酒店搜索 -->
    <HotelSearch/>

    <!-- 介绍和地图 -->
    <el-row type="flex" class="hotel-description">

      <!-- 介绍 -->
      <el-col :span="14" style="padding:5px">
        <el-row type="flex" style="margin-bottom:20px">
          <!-- 区域 -->
          <el-col :span="3">区域：</el-col>
          <el-col :span="21">全部</el-col>
        </el-row>
        <!-- 攻略 -->
        <el-row type="flex" style="margin-bottom:20px">
          <el-col :span="3">攻略：</el-col>
          <el-col :span="21">北京，你想要的都能在这找到。博古通今，兼容并蓄，天下一城，如是帝都。 景点以故宫为中心向四处辐射；地铁便宜通畅，而且覆盖绝大多数景点。 由于早上有天安门升旗仪式，所以大多数人选择在天安门附近住宿。</el-col>
        </el-row>
        <!-- 均价 -->
        <el-row type="flex" >
          <el-col :span="3">均价：
            <el-tooltip
              class="item question"
              effect="dark"
              content="等级均价由平日价格计算得出，节假日价格会有上浮。"
              placement="top-start"
            >
              <span>?</span>
            </el-tooltip>
          </el-col>
          <el-col :span="21">
            <el-row type="flex">
              <el-col>
                <i class="el-icon-star-on" v-for="item in 3" :key="item" style="color:#f90"></i>
                  <span class="price-budget">¥332</span>
              </el-col>
              <el-col>
                <i class="el-icon-star-on" v-for="item in 4" :key="item" style="color:#f90"></i>
                  <span class="price-budget">¥521</span>
              </el-col>
              <el-col>
                <i class="el-icon-star-on" v-for="item in 5" :key="item" style="color:#f90"></i>
                  <span class="price-budget">¥768</span>
              </el-col>
            </el-row>
          </el-col>
        </el-row>
      </el-col>

      <!-- 酒店地图 -->
      <el-col :span="10">
        <HotelMap/>
      </el-col>

    </el-row>

    <!-- 酒店筛选 -->
    <HotelFilter/>

    <!-- 酒店列表 -->
    <HotelList/>

    <!-- 分页 -->
    <el-pagination
      background
      layout="prev, pager, next"
      :total="1000">
    </el-pagination>
  </div>
</template>

<script>
import HotelSearch from '@/components/hotel/hotelSearch'
import HotelMap from '@/components/hotel/hotelMap'
import HotelFilter from '@/components/hotel/hotelFilter'
import HotelList from '@/components/hotel/hotelList'
export default {
  components:{
    HotelSearch,
    HotelMap,
    HotelFilter,
    HotelList
  }
};
</script>
<style lang="less" scoped>
.container{
  width: 1000px;
  margin: 0 auto;
  color: #666;
  font-size: 14px;
  // 面包屑
  .breadcrumb{
    padding: 20px 0
  }
  .hotel-description{
    margin-bottom: 20px;
    // 均价问号提示
    .question{
      background-color: #ccc;
      display: inline-block;
      width: 14px;
      height: 14px;     
      border-radius: 50%;
      text-align: center;
      font-size: 12px;
      color: #fff;
    }
  }
}
// 分页
.el-pagination {
  padding: 20px 0 40px;
  display: flex;
  justify-content: flex-end;
}

</style>