<template>
  <div class="home">
     <header-yellow/>
     <div class="main">
       <div class="cateory">
         <ul class="categories">
           <li v-for="(item,index) in computedCategories" :key="item.id" @click="changeCategories(index)">
             <span :class="{'active':activeCategory===index}">{{item.name}}</span>
           </li>
         </ul>
       </div>
       <div class="productList">
         <div class="product-filter">
           <div class="filter-titles">
            <div @click="changeAllCateegories" :class="{'active':allCategories}">
              <span>全部分类</span><var>&nbsp;</var>
            </div>
            <div>
              <span>综合排序</span><var>&nbsp;</var>
            </div>
          </div>
           <div class="filter-items" v-show="allCategories">
             <ul>
               <li :class="{'active':activeCid === '全部分类'}">全部分类</li>
               <li v-for="{item,index} in computedCategories[activeCategory].cids" :key="item.cid_id" :class="{'active':activeCid === iten.name}">{{item.name}}</li>
             </ul>
         </div>
       </div>
        <ul class="productList-wrap">
          <li v-for="(item,index) in computedCategories[activeCategory].products" :key="item.id">
            <dl>
              <dt>
                <img :src="item.imgs.min">
              </dt>
              <dd class="nowrap product-item-title">{{item.name}}</dd>
              <dd class="product-specifics-wrap">
                <div class="product-specifics">
                  <span>{{item.unit}}ml</span>
                  <var>￥{{item.price}}</var>
                </div>
                <div class="product-operates">
                  <span class="inner">-</span>
                  <span class="product-operates-item">10</span>
                  <span class="inner">+</span>
                </div>
              </dd>
            </dl>
          </li>
        </ul>
     </div>
    </div>
  </div>
</template>
<script>
import HeaderYellow from '@/components/Header-yellow/Header-yellow'
export default {
  data(){
    return {
    activeCategory: 0,
    activeCid:'全部分类'
    }
  },
  components:{
    HeaderYellow
  },
  computed:{
    computedCategories(){
      if(this.$store.state.computedCategories.length > 0){
        return this.$store.state.computedCategories
      }else{
        return [{cids:[]}]
      }
    }
  },
  methods:{
    changeCategories(index){
      this.activeCategory = index
    },
    changeAllCateegories(){
      this.allCategories = !this.allCategories
    }
  }
}
</script>
<style lang="less" scoped>
.category{
  overflow: scroll;
  position: relative;
  height: 100%;
}
.categories{
  float: left;
  width: 23.4375%;
  font-size: 1.3rem;
}
.categories>li{
  padding: 0.3rem 0;
  text-align: center;
  box-sizing: border-box;
  border-bottom: 0.1rem solid #d9d9d9;
}
.categories>li>span{
  display: block;
  height: 3.4rem;
  line-height: 3.4rem;
  padding-left: 0.6rem;
}
.categories>li>span.active{
  border-left: 0.6rem solid #f0d001;
  padding-left: 0;
}
.productList{
  /*float: right;*/
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  width: 76%;
}
.product-filter{
  display: flex;
  display: -webkit-flex;
  flex-direction:column;
  -webkit-flex-direction:column;
  position: absolute;
  z-index: 2;
  width: 100%;
}
.product-filter.active{
  height: 100%;
}
.filter-titles{
  height: 1.8rem;
  padding: 1.1rem 0;
  background-color: rgba(255,255,255,0.8);
  width: 100%;
  border-bottom: 0.1rem solid #e1dbdd;
}
.filter-titles>div{
  float: left;
  width: 50%;
  height: 1.8rem;
  line-height: 1.8rem;
  text-align: center;
  font-size: 1.2rem;
}
.filter-titles>div:nth-child(1){
  box-sizing:border-box;
  border-right: 0.1rem solid #d5d5d5;
}
.filter-titles>div>var{
  display: inline-block;
  width: 1.3rem;
  height: 1.8rem;
  line-height: 1.8rem;
  background: url("./images/icon-down.png") center center no-repeat;
  -webkit-background-size: 1rem 0.6rem;
  background-size: 1rem 0.6rem;
  -webkit-transition: 0.5s ease;
  -o-transition: 0.5s ease;
  transition: 0.5s ease;
  -webkit-transform: rotate(0deg);
  -ms-transform: rotate(0deg);
  -o-transform: rotate(0deg);
  transform: rotate(0deg);
}
.filter-titles>div.active>var{
  -webkit-transform: rotate(-180deg);
  -ms-transform: rotate(-180deg);
  -o-transform: rotate(-180deg);
  transform: rotate(-180deg);
}
.filter-items{
  flex:1;
  -webkit-flex:1;
  width: 100%;

  background-color: rgba(0,0,0,0.2);
}
.filter-items>ul{
  overflow: hidden;
  padding-bottom: 1rem;
  background-color: rgba(255,255,255,1);
}
.filter-items>ul>li{
  padding: 0.7rem 0.9rem;
  border: 0.1rem solid #e0e0e0;
  /*border: 0.1rem solid #e6d056;*/
  border-radius: 0.4rem;
  float: left;
  margin: 0.8rem 0 0 0.8rem;
  
}
.filter-items>ul>li.active{
  background-color: #fff9d9;
  border-color: #e6d056;
}
.productList-wrap{
  position: absolute;
  top: 4.1rem;
  bottom: 0;
  width: 100%;
  overflow-y: scroll;
  background-color: #fff;
}
.productList-wrap>li{
  border-bottom: 0.1rem solid #e1dbdd;
  padding: 0.8rem 1rem;
}
.productList-wrap>li>dl{
  overflow: hidden;
}
.productList-wrap>li>dl>dt{
  float: left;
  width: 8rem;
  height: 8rem;
  margin-right: 1rem;
  overflow: hidden;
  text-align: center;
}
.productList-wrap>li>dl>dt>img{
  width: 100%;
}
.productList-wrap>li>dl>dd{
  font-size: 1.2rem;
}
.product-item-title{
  margin-bottom: 2.5rem;
}
.product-specifics-wrap{
  overflow: hidden;
}
.product-specifics{
  float: left;
  width: 30%;
  overflow: hidden;
}
.product-specifics>span{
  display: block;
  color: #858585;
  margin-bottom: 1rem;
}
.product-specifics>var{
  color: #f40;
}
.product-operates{
  float: right;
  width: 70%;
  overflow: hidden;
}
.product-operates>.inner{
  display: inline-block;
  font-size: 2.5rem;
  width: 2rem;
  height: 2rem;
  line-height: 2rem;
  color: #d73e00;
  text-align: center;
  border: 0.1rem solid #dcbd9e;
  border-radius: 50%;
  padding: 0.8px;
}
.product-operates-item{
  display: inline-block;
  height: 1.9rem;
  line-height: 1.9rem;
  vertical-align: top;
  font-size: 1.2rem;
}
</style>



