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
    <HotelSearch @setCity="setCity" />

    <!-- 介绍和地图 -->
    <el-row type="flex" class="hotel-description">
      <!-- 介绍 -->
      <el-col :span="14" style="padding:5px">
        <el-row type="flex" style="margin-bottom:20px">
          <!-- 区域 -->
          <el-col :span="3">区域：</el-col>
          <el-col :span="21">
            <div id="scenics-box">
              <a href>全部</a>
              <a
                href="#"
                v-for="(item,index) in scenics"
                :key="index"
                class="location-budget"
              >{{item.name}}</a>
            </div>
            <a @click="openScenics">
              <i class="el-icon-arrow-down" style="color: #f90"></i>
              <span>等{{scenics.length}}个区域</span>
            </a>
          </el-col>
        </el-row>
        <!-- 攻略 -->
        <el-row type="flex" style="margin-bottom:20px">
          <el-col :span="3">攻略：</el-col>
          <el-col
            :span="21"
          >北京，你想要的都能在这找到。博古通今，兼容并蓄，天下一城，如是帝都。 景点以故宫为中心向四处辐射；地铁便宜通畅，而且覆盖绝大多数景点。 由于早上有天安门升旗仪式，所以大多数人选择在天安门附近住宿。</el-col>
        </el-row>
        <!-- 均价 -->
        <el-row type="flex">
          <el-col :span="3">
            均价：
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
        <HotelMap />
      </el-col>
    </el-row>

    <!-- 酒店筛选 -->
    <HotelFilter @setDataList="setDataList" />

    <!-- 酒店列表 -->
    <HotelList :data="hotels" />

    <!-- 分页 -->
    <el-pagination
      @current-change="handleCurrentChange"
      background
      layout="prev, pager, next"
      :total="total"
    ></el-pagination>
  </div>
</template>

<script>
import HotelSearch from "@/components/hotel/hotelSearch";
import HotelMap from "@/components/hotel/hotelMap";
import HotelFilter from "@/components/hotel/hotelFilter";
import HotelList from "@/components/hotel/hotelList";
export default {
  components: {
    HotelSearch,
    HotelMap,
    HotelFilter,
    HotelList
  },
  data() {
    return {
      name: "南京市",
      // 区域
      scenics: [],
      // 区域展开
      open: false,
      // 酒店数据列表
      hotels: [],
      //分页
      pageSize: 10,
      pageIndex: 1,
      total: 0
    };
  },
  methods: {
    //获取酒店列表数据
    getHotelData() {
      this.$axios({
        url: "/hotels",
        params: {
          _limit: this.pageSize,
          _start: (this.pageIndex - 1) * this.pageSize,
          ...this.$route.query
        }
      }).then(res => {
        if (res.status === 200) {
          // console.log(res.data);
          const { data, total } = res.data;
          this.hotels = data;

          //总页数
          this.total = total;
          this.pageIndex = 1;
        }
      });
    },
    //当前页
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`);
      this.pageIndex = val;
      this.getHotelData();
    },
    // 展开区域
    openScenics() {
      if (this.open == false) {
        document.getElementById("scenics-box").style.height = "auto";
        this.open = !this.open;
      } else {
        document.getElementById("scenics-box").style.height = "40px";
        this.open = !this.open;
      }
    },
    // 头部搜索
    setCity(value, name, content) {
      if (value) {
        const query = { city: value };
        this.$router.push({
          path: "/hotel",
          query
        });
        this.$axios({
          url: "/hotels",
          query
        }).then(res => {
          if (res.status === 200) {
            // console.log(res.data);
            const { data, total } = res.data;
            this.hotels = data;

            //总页数
            this.total = total;
            this.pageIndex = 1;
          }
        });
      } else {
        this.$router.push({
          path: "/hotel",
          query:''
        });
      }
    },
    //筛选酒店数据
    setDataList(obj) {
      let query = { ...this.$route.query, ...obj };
      const { price_lt, hotellevel, hoteltype, hotelasset, hotelbrand } = query;
      if (price_lt == 0) {
        delete query.price_lt;
      }
      if (!hotellevel) {
        delete query.hotellevel;
      }
      if (!hoteltype) {
        delete query.hoteltype;
      }
      if (!hotelasset) {
        delete query.hotelasset;
      }
      if (!hotelbrand) {
        delete query.hotelbrand;
      }

      // console.log(query);
      this.$router.push({
        path: "/hotel",
        query
      });
    }
  },
  mounted() {
    this.getHotelData();

    // 获取区域
    this.$axios({
      url: `/cities?name=${this.name}`
    }).then(res => {
      // console.log(res.data.data[0].scenics);
      this.scenics = res.data.data[0].scenics;
    });
  },
  watch: {
    $route() {
      setTimeout(() => {
        this.getHotelData();
      }, 10);
    }
  }
};
</script>
<style lang="less" scoped>
.container {
  width: 1000px;
  margin: 0 auto;
  color: #666;
  font-size: 14px;
  // 面包屑
  .breadcrumb {
    padding: 20px 0;
  }
  .hotel-description {
    margin-bottom: 20px;
    #scenics-box {
      height: 40px;
      overflow: hidden;
      a:hover {
        background-color: #eee;
      }

      .location-budget {
        margin-right: 1em;
        padding: 0 2px;
        border-radius: 4px;
        display: inline-block;
        cursor: pointer;
      }
    }
    // 均价问号提示
    .question {
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