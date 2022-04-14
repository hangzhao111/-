<template>
  <div>
    <div class="f11">
      <div class="f1">
        <span class="left">产品中心</span>
        <span class="right">
          <a href="">婚礼花艺</a>
          <em>|</em>
          <a href="">爱情鲜花</a>
          <em>|</em>
          <a href="">长辈鲜花</a>
        </span>
      </div>
    </div>
    <div class="f2">
      <div class="container1">
        <button class="btn1">求婚必备</button>
        <button class="btn2">情人节专属</button>
        <button class="btn3">其他鲜花</button>
      </div>
    </div>
  <!-- 三楼样式 -->
  <div class="f3">
    <div class="container">
      <div class="c1" v-for="v in data.result" :key="v.uid">
        <div id="tuPian">
        <img :src=v.pic alt="">
        </div>
        <div class="cc10"><p class="red">{{v.title}}</p>
            <p class="red1">
              <em>￥</em>
              {{v.price}}
            </p></div>
      </div>
    </div>
  </div>


    <!-- <div class="f3">
      <div class="container">
        <div class="c1" v-for="v in data" :key="v.uid">
          <img :src="v.pic" alt="" />
          <div class="cc10">
            <p class="red">{{v.title}}</p>
            <p class="red1">
              <em>￥</em>
              {{v.price}}
            </p>
          </div>
        </div> -->

        <!-- <div class="c2">
          <img src="/imgbs/2.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c3">
          <img src="/imgbs/3.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em> ￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c4">
          <img src="/imgbs/4.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c5">
          <img src="/imgbs/5.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c6">
          <img src="/imgbs/6.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em> ￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c7">
          <img src="/imgbs/7.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>

        <div class="c8">
          <img src="/imgbs/8.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c9">
          <img src="/imgbs/9.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div>
        </div>
        <div class="c10">
          <img src="/imgbs/10.jpg" alt="" />
          <div class="cc10">
            <p class="red">海洋之心</p>
            <p class="red1">
              <em>￥</em>
              399
            </p>
          </div> 
        </div>
      </div>
    </div>-->
    <div class="f4">
      <div class="container">
        <!-- 分页条 -->
       <div id="page" v-if="data">
         <span>上一页</span>
         <span 
         @click="getData(p)"
         :class="{cur:pageNum==p}"
         v-for="p in sum " :key="p">{{p}}</span>
         <span>下一页</span>
       </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // props: {
  //           pageNum: {
  //               type: String,  //类型是 字符串
  //               default: '',  //默认值是空字符串
  //           },
  //       },

   data() {
    
    return {
                data: null,
                sum: null,
            }
  },
 mounted(){
   this.data
  this.getData()
 },
 methods:{
   getData(pageNum=1){
      let url = `http://127.0.0.1:8088/v2/product/list?pageSize=8&pageNum=${pageNum}`
      console.log('url:',url);
    this.axios.get(url).then((res)=>{
      this.data = res.data
      console.log(res.data)
      let c = res.data.result1[0].count
      let b = c/8
      this.sum=Math.ceil(b)
    })
   },
 },
};
</script>
 <style scoped src="../assets/reset.css"></style>
<style scoped src="../assets/css/MiYol.css"></style>
<style lang="scss">
</style>
