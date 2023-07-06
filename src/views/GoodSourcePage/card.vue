<template>

      <el-card :body-style="{ padding: '0px' }" class="card" >
        <div style="height: 210px;">

          <!-- 图片的div -->
          <div style="height: 180px">
            <img
                :src="pet.imgPath"
                class="image"
            />
          </div>

          <!-- 两个按钮的div -->
          <div style="text-align: right">
            <el-tooltip
                class="box-item"
                effect="dark"
                content="加入购物车"
                placement="top-start"
            >
              <ShoppingCart  class="icon" @click="toCart"/>
            </el-tooltip>
            <el-tooltip
                class="box-item"
                effect="dark"
                content="查看详情"
                placement="top-start"
            >
              <DArrowRight class="icon" @click="toDetail"/>
            </el-tooltip>
          </div>
        </div>


        <div style="padding:20px;margin-top: -30px;height: 130px">
          <span style="font-weight: bold;font-size: 15px;">{{this.pet.name}}</span>
          <div class="bottom">
            <paragraph style="letter-spacing:2px;line-height: 20px">{{this.pet.description}}</paragraph>
          </div>
        </div>
        <div style="display:flex;padding: 20px 15px">
          <div style="width: 50%;text-align: left">
            <Icon type="md-cart" style="color:#929191"/>&nbsp
            <text style="color:#929191">{{this.pet.price}}￥</text>
          </div>
          <div style="width: 50%;text-align:right">
            <Icon type="md-flame" style="color:#929191"/>
            <text style="color:#929191">{{this.pet.sales}}</text>
          </div>
        </div>

      </el-card>

</template>

<script >

import request from "@/assets/utils/request";

export default {


  name: "imageList",
  components:{
  },
  data(){
    return{
      claw:require("@/assets/1.png"),
      categoryName:'',
      detail:false
    }
  },
  props: {
    pet: Object,
  },
  methods:{
    toDetail(){
      let data = JSON.stringify(this.pet) // result传递的query参数。我们转为string
      if(this.detail)
        this.$router.push({path: '/detail', query: {res: data}})
      else
        this.$message({
          type: "error",
          message: "数据库中没有关于这个商品的详情"
        })
    },
    toCart(){
      const cart= {
        username: JSON.parse(sessionStorage.getItem("user")).username,
        productId: this.pet.productId,
        name:this.pet.name,
        price:this.pet.price,
        categoryName:this.categoryName,
        quantity: 1
      }
      request.post("/cart/save", cart).then(res =>{
        if (res.code === '0') {
          this.$message({
            type: "success",
            message: "加入成功，快去看看吧"
          })
        }
      })
    }
  },
  mounted() {

    request.get("/detail/select/"+ this.pet.productId).then(res =>{

      console.log(this.productId+"   "+res.code)
      if(res.code ==='-1'){
        console.log(res.msg);
        return
      }
      this.detail =true
      const cate = res.data.outerList
      cate.forEach(item =>{
        this.categoryName +=item.valueGroup[0];
        this.categoryName +=" ";
      })
    })

  }

}

</script>

<style scoped>
.time {
  font-size: 12px;
  color: #999;
}

.bottom {
  margin-top: 5px;
  line-height: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  text-align: left
}

.button {
  padding: 0;
  min-height: auto;
}

.image {
  height: 100%;
  display: block;
}

.icon{
  padding: 0.5em;
  width: 2.5em;
  height: 2.5em;
  color: white;
  background-color: orange;
  border-radius: 50%;
  box-shadow: 0.1em 0.1em 0.1em  #888888;
  margin-top: -15px;
  margin-right: 7px;
}

.icon:hover{
  box-shadow: 0.2em 0.2em 0.2em  #888888;
  padding: 0.4em;
}

.card{
  margin: 10px 0px;height:360px
}

.card:hover{
  box-shadow:0em 0em 1em  #888888;
}
</style>


<!--
<img  :src="require(`@/assets/page2/products/${petname}.jpg`)" />
这种写法也可以引进来图片，所以这样子就可以加变量了



-->
