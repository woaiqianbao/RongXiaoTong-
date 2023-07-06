<!--商品货源-->
<template>
  <div style="">

    <img src="../../assets/page2/background2.jpg" alt="">
    <Subtitle subtitle="商品列表" description="买到就是赚到哦~"  style="margin-top:100px;"/>

    <div class="home-goods">
    <goods-sourse :cgoods="goods" @handleSearch="handleSearch"></goods-sourse>

<!--      <pagination @item-click="pageClick" :cUrl="url" :cTotal="total" :cPageSize="pageSize"></pagination>-->
  </div>
  </div>

</template>

<script>
import { selectGoodsPage } from "../../api/order";
import GoodsSourse from "./GoodsSource.vue";
import Pagination from "../../components/Pagination";
import Subtitle from "../../components/Subtitle";

export default {
  data() {
    return {
      goods: [],
      total: 0,
      pageSize: 30,
      searchValue:'',
      url: "/order/goods/",
      goodsCount: sessionStorage.getItem("/order/goods/pageCode")
        ? sessionStorage.getItem("/order/goods/pageCode")
        : 1,
    };
  },
  mounted() {
    this.$store.commit("updateActiveIndex", "2");
    this.getData()
  },
  methods: {
    getData(){
      selectGoodsPage({
        pageNum: this.goodsCount,
        keys:this.searchValue
      }).then((res) => {
        if (res.flag == true) {
          this.goods = res.data.list;
          this.total = res.data.total;
        } else {
          // alert(res.data.data);
        }
      });
    },
    pageClick(item) {
      this.goods = item;
    },
    handleSearch(val){
      this.searchValue = val
      this.getData()
    }
  },
  components: {
    Pagination,
    GoodsSourse,
    Subtitle
  },
};
</script>

<style lang="less" scoped>
.home-goods {
  width: 1100px;
  margin: 0 auto;
}


</style>
