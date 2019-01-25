<template>
    <div class="chooseBox">
        <div class="title">筛选</div>
        <div class="choose">
            <div class="sbuTitle clearfix">
                <span class="fll">投资方式</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow" @click="handleShowList"></i>  
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList"></i>  
            </div>
            <div class="type" v-show="isShow">
                <span v-for="(item,index) in investTypeList" :key="index" :class="{active:isActive == index}" @click="checkItem(index)">{{item.dataName}}</span>
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">资金类型（可多选）</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow1" @click="handleShowList1"></i>  
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList1"></i>  
            </div>
            <div class="type" v-show="isShow1">
                <van-checkbox-group v-model="result">
                    <van-checkbox v-for="(item, index) in regionList" :key="index" :name="item" class="checkItem" checked-color="#005982">
                        {{ item.dataName }}
                    </van-checkbox>
                </van-checkbox-group>
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">投资行业（可多选）</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow2" @click="handleShowList2"></i>  
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList2"></i>  
            </div>
            <div class="type" v-show="isShow2">
                <van-checkbox-group v-model="result">
                    <van-checkbox v-for="(item, index) in investIndustryList" :key="index" :name="item" class="checkItem" checked-color="#005982">
                        {{ item.dataName }}
                    </van-checkbox>
                </van-checkbox-group>
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">投资地区</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow3" @click="handleShowList3"></i>  
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList3"></i>  
            </div>
            <div class="type" v-show="isShow3">
                 <span v-for="(item,index) in investRegionList" :key="index" :class="{active:isActive3 == index}" @click="checkItem3(index)">{{item.dataName}}</span>
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">投资金额</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow4" @click="handleShowList4"></i>  
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList4"></i>  
            </div>
            <div class="type" v-show="isShow4">
                 <span v-for="(item,index) in investAmountList" :key="index" :class="{active:isActive4 == index}" @click="checkItem4(index)">{{item.dataName}}</span>
            </div>
        </div>
        <div class="clearfix sureChoose">
            <mu-button class="chooseBtn fll">清空</mu-button>
            <mu-button class="chooseBtn flr sure">确定</mu-button>
        </div>
    </div>

</template>

<script>
    export default {
        data() {
            return {
                isShow:false,
                isShow1:false,
                isShow2:false,
                isShow3:false,
                isShow4:false,
                isActive:0,
                isActive3:0,
                isActive4:0,
                result: [],
                typeList:["全部","债权融资","股权融资","整体转让","其他融资"],
                moneyType: ["个人资金", "企业资金", "天使投资", "VC投资", "PE投资", "小额贷款", "典当公司"],
                investAmountList:[],
                investIndustryList:[],
                investRegionList:[],
                investTypeList:[],
                regionList:[]
            };
        },
        methods:{
            handleShowList(){
                this.isShow = true
                
            },
            handleCloseList(){
                this.isShow = false
            },
            handleShowList1(){
                this.isShow1 = true
                
            },
            handleCloseList1(){
                this.isShow1 = false
            },
            handleShowList2(){
                this.isShow2 = true
                
            },
            handleCloseList2(){
                this.isShow2 = false
            },
            handleShowList3(){
                this.isShow3 = true
                
            },
            handleCloseList3(){
                this.isShow3 = false
            },
            handleShowList4(){
                this.isShow4 = true
                
            },
            handleCloseList4(){
                this.isShow4 = false
            },
            checkItem(item) {
                this.isActive = item
            },
            checkItem3(item) {
                this.isActive3 = item
            },
            checkItem4(item) {
                this.isActive4 = item
            },
            getType(){
                this.$axios.get(`/jsp/wap/trCapital/ctrl/jsonCategoryList.jsp`).then(res=>{
                    console.log("yyy",res)
                    this.investAmountList = res.data.investAmountList
                    this.investIndustryList = res.data.investIndustryList
                    this.investRegionList = res.data.investRegionList
                    this.regionList = res.data.regionList
                    this.investTypeList = res.data.investTypeList
                })
            }
        },
        created(){
            this.getType()
        }
    };
</script>
<style scoped lang="scss">
    .chooseBox {
        background: #fff;
        // height: 100vh;
    }

    .choose {
        overflow: scroll;
        height: 100vh;
        padding-bottom: 2rem
    }

    .title {
        text-align: center;
        line-height: 3;
        border-bottom: 1px solid #f3f5f7
    }

    .sbuTitle {
        font-size: .28rem;
        font-family: "PingFang";
        color: rgb( 51, 51, 51);
        font-weight: bold;
        line-height: 4;
        padding: 0 .2rem;
        border-bottom: 1px solid #f3f5f7;
    }

    .type {
        display: flex;
        flex-wrap: wrap;
        border-bottom: 1px solid #f3f5f7;
        padding: .2rem .2rem .3rem;
    }

    .type span {
        background: #eee;
        width: 2.6rem;
        text-align: center;
        padding: .1rem .15rem;
        border-radius: 10%;
        margin-right: .2rem;
        margin-top: .2rem;
        font-size: .24rem;
        font-family: "PingFang";
        color: rgb( 102, 102, 102);
    }
    .type span.active {
        background: #005982;
        color: #fff;
    }
    .checkItem{
        line-height: 2,
        
    }

    .sureChoose {
        position: absolute;
        width: 100%;
        bottom: 0;
    }

    .chooseBtn {
        width: 50%;
        padding: .6rem 0;
        font-size: .3rem;
    }

    .sure {
        background: #005982;
        color: #fff
    }
    /* 多选框 */
    #moneyType{
        width: 2rem
    }
</style>