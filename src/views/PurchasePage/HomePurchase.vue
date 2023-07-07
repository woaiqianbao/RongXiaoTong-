<template>
  <div>
    <img src="../../assets/page3/background3.jpg" alt="">
    <Subtitle subtitle="需求列表" description="买到就是赚到哦~"  style="margin-top:100px;"/>

    <div class="home-purchase">
      <purchase :cneeds="needs" @handleSearch="handleSearch"></purchase>
      <pagination
          @item-click="pageClick"
          :cUrl="url"
          :cTotal="total"
          :cPageSize="pageSize"></pagination>
    </div>
  </div>

</template>

<script>
import { selectNeedsPage } from "../../api/order";
import Purchase from "./Purchase.vue";
import Pagination from "../../components/Pagination.vue";
import Subtitle from "../../components/Subtitle";
export default {
  data() {
    return {
      needs: [],
      total: 0,
      pageSize: 30,
      searchValue:"",
      url: "/order/needs/",
      needsCount: sessionStorage.getItem("/order/needs/pageCode")
        ? sessionStorage.getItem("/order/needs/pageCode")
        : 1,
    };
  },
  created() {
    this.$store.commit("updateActiveIndex", "3");
    this.getData()
  },
  methods: {
    getData(){
      selectNeedsPage({
        pageNum: this.needsCount,
        keys:this.searchValue
      }).then((res) => {
        if (res.flag == true) {
          this.needs = res.data.list;
          this.total = res.data.total;
        }
      });
    },
    pageClick(item) {
      this.needs = item;
    },
    handleSearch(val){
      this.searchValue = val
      this.getData()
    }
  },
  components: {
    Purchase,
    Pagination,
    Subtitle
  },
};
</script>

<style lang="less" scoped>
.home-purchase {
  width: 1500px;
  margin: 0 auto;
}
</style>;
