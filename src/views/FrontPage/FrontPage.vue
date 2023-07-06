<template>
  <div class="front-container" m="t-4">
    <Carousel></Carousel>
    <Search></Search>
    <OurService></OurService>
    <HotSales></HotSales>
    <AboutUs />

    <el-menu
        mode="horizontal"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b" style="height:200px;margin-bottom: -50px" >
      <el-menu-item index="1" style="margin-left:14%;width:25%" >
        <div>
          <div style="width: 100%"><Location style="width:30px; height:30px;"  /></div>
          <div style="width: 100%">地址: 山东省 济南市 历下区 山东大学软件园校区</div>
    </div>
      </el-menu-item>
      <el-menu-item index="2" style="width:25%">
        <div>
          <div style="width: 100%"><Phone style="width:30px; height:30px;"  /></div>
          <div style="width: 100%">  联系电话: 13233138362</div>
    </div>
      </el-menu-item>
      <el-menu-item index="3" style="width: 25%">
        <div>
          <div style="width: 100%"><Message style="width:30px; height:30px;"  /></div>
          <div style="width: 100%">邮箱: 1837879652@qq.com</div>
  </div>
      </el-menu-item>


    </el-menu>
</div>

</template>
<script>
import OurService from "./OurService";
import HotSales from "./HotSales";
import Search from "./Search";
import Carousel from "./Carousel";
import AboutUs from "./AboutUs";

export default {
  components:{
    Carousel,
    OurService,
    HotSales,
    Search,
    AboutUs
  },

};
</script>

<style scoped>


.front-container{
  margin: 20px auto;
}



</style>
