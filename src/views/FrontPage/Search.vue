<template>

  <div class="search-container">
    <div class="left">
          <span>热门关键词：普通复合肥  |  腐植酸有机无机复合肥  |  控释肥  |  硫酸钾  |  水溶肥  |  叶面肥  |</span>
    </div>
    <div class="right">
      <el-input
          placeholder="请输入关键词"
          v-model="input">
        <i slot="prefix" class="el-input__icon el-icon-search"  ></i>
      </el-input>
    </div>

  </div>
</template>

<script>
export default {
  name: "Search",
  data(){
    return{
      input:''
    }
  }
}
</script>

<style scoped>

.search-container {
  background-color: #4ab344;
  width: 100%;
  height: 80px;
}

.left{
  position: relative;
  color: #ffffff;
  font-size: 16px;
  top: 30px;
  left: 200px;
}


.right{
  position: relative;
  width: 15%;

  left:75%;
}


</style>
