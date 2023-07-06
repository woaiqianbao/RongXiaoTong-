<template>
  <el-carousel class="demonstration" trigger="click" >
    <el-carousel-item v-for="item in imgList" :key="item.name">
      <img :src="item.src" style="height: 100%;" :title="item.title" />
    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  name: "Carousel",
  data() {
    return {
      imgList: [
        {
          name: "carousel1",
          src: require("@/assets/page1/Carouselimages/carousel1.jpg"),
        },
        {
          name: "carousel2",
          src: require("@/assets/page1/Carouselimages/carousel2.jpg"),
        },
      ]
    };
  },
}
</script>

<style scoped>
/*设置走马灯宽度*/
.demonstration {
  width: 100%;
}

/*设置走马灯高度*/
::v-deep .el-carousel__container  {
  position: relative;
  height: 600px;
}


/deep/.el-carousel__indicators--horizontal {
  position: absolute;
  left: auto;
  right: 42%;
  bottom: 10px;
  text-align: right;
}

/deep/ .el-carousel__indicator--horizontal button {
  width: 70px;
  height: 5px;
  background: #ffffff;
  border-radius: 5px;

}

/deep/ .el-carousel__indicator--horizontal.is-active button {
  width: 70px;
  height: 5px;
  background: #ffffff;
  border-radius: 3px;
}
</style>
