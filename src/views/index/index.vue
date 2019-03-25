<template>
<div class="index">
  <div class="clearfix w1170">
    <Banner></Banner>
    <UserBox></UserBox>
  </div>
  <div class="w1170">
    <div class="article-list" v-if="userInfo.username">
      <router-link :to="{name: 'article', params: {id: item._id}}" class="item" v-for="item in content" :key="item.id">
        <div class="item-top">
          <div class="img-wrap">
            <img :src="item.author.avatar">
          </div>
          <div class="item-msg">
            <div class="row-one">
              <span class="author-name">
                {{item.author.username}}
              </span>
              <span class="divide">|</span>
              <span class="article-title">
                {{item.title}}
              </span>
            </div>
            <div class="row-two">
              <span class="row-item">
                浏览:<span>{{item.readnumber}}</span>
              </span>
              <span class="row-item">
                回复:<span>{{item.readnumber}}</span>
              </span>
              <span class="row-item">
                分类:<span>{{item.category.name}}</span>
              </span>
            </div>
          </div>
        </div>
        <div class="item-content">
          {{item.contentText}}
        </div>
      </router-link>
    </div>
  </div>
</div>
</template>

<script>
import Banner from '@/components/Banner'
import UserBox from '@/components/UserBox'
import {mapState} from 'vuex'

export default {
  components: {
    Banner,
    UserBox,
  },
  data() {
    return {
      content: []
    }
  },
  methods: {
    getData() {
      this.$axios.get('/article').then(res => {
        console.log(res.data)
        this.content = res.data
        console.log(this.content)
      })
    }
  },
  created() {
    this.getData()
  },
  computed: {
      ...mapState(['userInfo'])
    }
}
</script>

<style scoped lang="scss">
.index {
  margin-top: 50px;

  .article-list {
    width: 750px;
    box-sizing: border-box;
    margin-top: 30px;
    border-radius: 6px;
    padding: 2px 20px;
    background: #fff;
  }
  .item {
    text-decoration: none;
    color: #333;
    display: block;
    padding-bottom: 10px;
    margin-top: 10px;
  }
  .item-top {
    display: flex;
    .img-wrap {
      width: 70px;
      height: 70px;
      img {
        display: block;
        width: 100%;
        height: 100%;
        border-radius: 4px;
      }
    }
  }
  .row-one {
    display: flex;
    line-height: 24px;
    .author-name {
      color: #409eff;
      font-weight: 700;
      padding-right: 8px;
      font-size: 18px;
    }
    .article-title {
      font-weight: 700;
      padding-left: 10px;
      font-size: 18px;
    }
  }
  .item-msg {
    width: 100%;
    margin-left: 15px;
  }
  .row-two {
    box-sizing: border-box;
    padding: 4px 8px;
    margin-top: 15px;
    border-radius: 4px;
    width: 100%;
    background: #bbb;
    .row-item {
      font-size: 14px;
      color: #555;
      font-weight: 700;
      margin-right: 30px;
    }
  }
  .item-content{
    margin-top: 10px;
  }
}
</style>
