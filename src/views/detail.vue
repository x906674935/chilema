<template>
    <div class="detail">
        <div class="head">
            <span class="back" @click="back"> back </span>
            <span>{{foodList.name}}</span>
        </div>
        <div class="content">
            <div class="imgbox">
                <img :src="imgsrc+foodList.image_path" alt="">
            </div>
            <p class="description">{{foodList.description}}</p>
            <div class="info">
                <p class="name">{{foodList.name}}</p>
                <p class="rating">评分 <span>{{foodList.rating}}</span> </p>
                <p class="tips">{{foodList.tips}}</p>
                <p class="satisfy">好评率  {{foodList.satisfy_rate}}%</p>
            </div>
        </div>
    </div>
</template>
<script>
import Axios from 'utils/axios';
export default {
    data() {
        return {
            foodList : [],
            imgsrc : '//elm.cangdu.org/img/',
            restuarantid : 3269,
            foodid : 1667
        }
    },
    methods: {
        back(){
            this.$router.go(-1)
        },
        initFoodData(){
            Axios.get(`https://elm.cangdu.org/shopping/v2/menu?restaurant_id=${this.restuarantid}`)
            .then((res)=>{
                
                //this.foodList = res[0].foods[1]
                
                for (let index = 0; index < res.length; index++) {
                   for (let k = 0; k < res[index].foods.length; k++) {
                       if(res[index].foods[k].item_id == this.foodid)
                        this.foodList = res[index].foods[k]
                   }
                    
                }
              
            })
        }
    },
    created() {
        this.restuarantid = this.$route.query.shopId
        this.foodid = this.$route.query.address
        
    },
    mounted() {
        this.initFoodData()
      
    },
}
</script>
<style lang="less" scoped>
 @import '~style/index.less';
 .detail{
     position: fixed;
     .top(0);
     .bottom(0);
     .w(375);
     z-index:2;
     background:white;
     .head{
         .w(375);
         .h(46);
         background: #3190E8;
         display: flex;
         justify-content: center;
         .l_h(46);
         .f_s(18);
         color: #fff;
         position: relative;
        .back{
            position: absolute;
            .left(5)
        }
     }
     .content{
         .imgbox{
             .w(375);
             .h(375);
             img{
                 width: 100%;
             }
         }
         .description{
             .h(18);
             .w(375);
             .margin(12,0,12,0);
             .f_s(14);
             .padding(0,10,0,10);
         }
         .info{
             .w(375);
             .h(120);
             .padding(0,12,12,12);
             .f_s(14);
             p{
                 .h(28);
             }
             .name{
                 .h(20);
                 .f_s(16);
                 color: #333;
                 .margin(5,0,5,0);
             }
             .rating{
                 span{
                     color: #f60;
                     .f_s(12);
                 }
             }
             .tips{

             }
             .satisfy{
                 .f_s(14);
                 color: #666;
             }
         }
     }
 }
</style>
