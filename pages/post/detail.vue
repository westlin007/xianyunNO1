<template>
  <!-- 攻略详情页 -->
  <section class="container">
    <el-row type="flex" justify="space-between">
      <div class="main">
        <!-- 面包屑导航 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
          <el-breadcrumb-item :to="{ path: '/post' }">游戏攻略</el-breadcrumb-item>
          <el-breadcrumb-item>攻略详情</el-breadcrumb-item>
        </el-breadcrumb>

        <!-- 标题 , 信息-->
        <h1>{{article.title}}</h1>
        <div class="post-info">
          <span>攻略：{{city.created_at}}</span>
          <span>阅读：{{article.watch}}</span>
        </div>

        <!-- 详细内容 -->
        <div class="post-content" v-html="article.content">{{article.content}}</div>

        <div>
          <Comments />
        </div>

        <!-- 提交评论 -->
        <div>
          <PostComments />
        </div>

        <!-- 获取评论 -->
        <GetComment />
      </div>

      <div class="aside">
        <h4>相关攻略</h4>
		<div class="recommend" v-for="(item,index) in recommend" :key="index">
		  <nuxt-link :to="`/post/detail?id=${item.id}`">
		    <div class="recommend_list">
		      <div class="recommend_left">
		        <img :src="item.images[0]" alt />
		      </div>
		      <div class="recommend_right">
		        <div class="recommend_tittle">{{item.title}}</div>
		        <p class="recommend_read">{{item.updated_at}} 阅读 {{item.watch}}</p>
		      </div>
		    </div>
		  </nuxt-link>
		</div>
      </div>
    </el-row>
  </section>
</template>

<script>
import Comments from "@/components/post/comment.vue";
import PostComments from "@/components/post/PostComments.vue";
import GetComment from "@/components/post/GetComment.vue";
export default {
  data() {
    return {
      article: {
        title: "",
        content: "",
        watch: ""
      }, //文章详情信息总数据

      account: {}, //z账户信息
      city: {
        created_at: ""
      },
      Comments: {} //评论信息
    };
  },
  components: {
    Comments,
    PostComments,
    GetComment
  },
  mounted() {
    const id = this.$route.query.id;
    this.$axios({
      url: "/posts?id=" + id
    }).then(res => {
      this.article = res.data.data[0];
      const { account, city, Comments } = res.data.data[0];
      this.account = account;
      this.city = city;
      this.Comments = Comments;

      // console.log(this.article);
    });
	this.$axios({
	  url: "posts/recommend",
	  parmas: { id: this.$route.query.id }
	}).then(res => {
	  this.recommend = res.data.data;
	  this.recommend.forEach((item, index) => {
	    item.updated_at = moment(item.updated_at).format("YYYY-MM-DD HH:mm");
	  });
	});
  },
  watch: {
    $route() {
      this.$axios({
        url: "/posts",
        params: { id: this.$route.query.id }
      }).then(res => {
        this.detail = res.data.data[0];
        this.detail.updated_at = moment(this.detail.updated_at).format(
          "YYYY-MM-DD HH:mm"
        );
      });
      this.$axios({
        url: "posts/recommend",
        parmas: { id: this.$route.query.id }
      }).then(res => {
        this.recommend = res.data.data;
        this.recommend.forEach((item, index) => {
          item.updated_at = moment(item.updated_at).format("YYYY-MM-DD HH:mm");
        });
      });
    }
  }
};
</script>

<style lang="less" scoped>
.container {
  width: 1000px;
  margin: 0 auto;
  padding: 20px 0;
  .main {
    width: 700px;

    h1 {
      padding: 20px 0;
      border-bottom: 1px solid #ddd;
      font-size: 32px;
    }
    .post-info {
      padding: 20px 0;
      color: #999;
      text-align: right;
    }
  }

  .aside {
    width: 280px;
    height: 300px;
    h4 {
      border-bottom: 1px solid #ddd;
      color: #999;
    }
	.recommend {
	  a {
	    .recommend_list {
	      display: flex;
	      padding: 20px 0px;
	      border-bottom: 1px solid #999;
	      .recommend_left {
	        img {
	          width: 100px;
	          height: 80px;
	          margin-right: 10px;
	        }
	      }
	      .recommend_right {
	        position: relative;
	        overflow: hidden;
	        .recommend_tittle {
	          width: 170px;
	          height: 45px;
	          font-size: 16px;
	          overflow: hidden;
	        }
	        .recommend_read {
	          font-size: 12px;
	          color: #999;
	          position: absolute;
	          left: 0;
	          bottom: 0;
	        }
	      }
	    }
	  }
	}
	
  }
}
</style>
