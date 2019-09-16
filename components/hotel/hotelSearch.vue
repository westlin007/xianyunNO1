<template>
  <div>
    <el-form :inline="true" ref="form" :model="form">
      <!-- 城市 -->
      <el-autocomplete
        v-model="city"
        :fetch-suggestions="querySearchCity"
        placeholder="城市"
        @select="handleSelectCity"
      ></el-autocomplete>

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
      <el-select v-model="form.num" placeholder=" 0人 ">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        ></el-option>
      </el-select>

      <!-- 按钮 -->
      <el-form-item>
        <el-button type="primary" @click="queryPrice">查看价格</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      city:"",
      form: {
        cityId: "",
        date: "",
        num: ""
      },
      
      citList: [],
      options: [
        {
          value: "1",
          label: "1人"
        },
        {
          value: "2",
          label: "2人"
        },
        {
          value: "3",
          label: "3人"
        },
        {
          value: "4",
          label: "4人"
        },
        {
          value: "5",
          label: "5人"
        },
        {
          value: "6",
          label: "6人"
        }
      ]
    };
  },
  methods: {
    // 城市下拉列表
    querySearchCity(queryString, cb) {
      this.$axios({
        url: "/cities?name=" + queryString
      }).then(res => {
        // console.log(res);
        var cityList = res.data.data.map(v => {
          return {
            ...v,
            value: v.name
          };
        });
        var results = queryString
          ? cityList.filter(this.createFilter(queryString))
          : cityList;
        // 显示建议数据
        cb(results);
      });
    },
    createFilter(queryString) {
      return citylist => {
        return citylist.value
          .toLowerCase()
          .indexOf(queryString.toLowerCase() > -1);
      };
    },
    // 选择城市
    handleSelectCity(item) {
      this.city = item.value;
      this.form.cityId = item.id
    },
    queryPrice() {
      // this.$axios({
      //   url:`/hotels`,
      //   params:{
      //     city:this.form.cityId
      //   }
      // }).then(res=>{
      //   console.log(res);
      // })
      this.$emit("setCity",this.form.cityId);
    }
  }
};
</script>