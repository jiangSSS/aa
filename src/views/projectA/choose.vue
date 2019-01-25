<template>
    <div class="chooseBox">
        <div class="title">筛选</div>
        <div class="choose">
            <div class="sbuTitle clearfix">
                <span class="fll">融资方式</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow" @click="handleShowList"></i>
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList"></i>
            </div>
            <div class="type" v-show="isShow">
                <span class="radioItem" v-for="(item,index) in financingWayList" :key="index" :class="{active:isActive == index}" @click="checkItem(index)">{{item.dataName}}</span>
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">所属行业（可多选）</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow1" @click="handleShowList1"></i>
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList1"></i>
            </div>
            <div class="type" v-show="isShow1">
                    <van-checkbox-group v-model="result">
                            <van-checkbox v-for="(item, index) in industryList" :key="index" :name="item" class="checkItem" checked-color="#005982">
                                {{ item.dataName }}
                            </van-checkbox>
                        </van-checkbox-group>
                <!-- <span v-for="(item, index) in industryList" :key="index" class="checkBtn" :class="(item.like == 0 ? ' nolike' : ' like')" @click="checkItem1(index)">{{item.dataName}}</span> -->
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">所在地区（可多选）</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow2" @click="handleShowList2"></i>
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList2"></i>
            </div>
            <div class="type" v-show="isShow2">
                    <van-checkbox-group v-model="result">
                            <van-checkbox v-for="(item, index) in regionList" :key="index" :name="item" class="checkItem" checked-color="#005982">
                                {{ item.dataName }}
                            </van-checkbox>
                        </van-checkbox-group>
                <!-- <span v-for="(item, index) in regionList" :key="index" class="checkBtn" :class="(item.like == 0 ? ' nolike' : ' like')" @click="checkItem2(index)">{{item.dataName}}</span> -->
                <!-- <label v-for="(item, index) in regionList" :key="index" class="checkBtn" :class="{active:isActive2 == true}" @click="checkItem2(index)"><input type="checkbox">{{item.dataName}}</label> -->
            </div>
            <div class="sbuTitle clearfix">
                <span class="fll">融资金额</span>
                <i class="iconfont icon-xiangxia flr" v-if="!isShow3" @click="handleShowList3"></i>
                <i class="iconfont icon-xiangshang flr" v-else @click="handleCloseList3"></i>
            </div>
            <div class="type" v-show="isShow3">
                <div v-for="(item, index) in financingMoneyList" :key="index" class="radioItem" :class="{active:isActive3 == index}" @click="checkItem3(index)">{{item.dataName}}</div>
            </div>
        </div>
        <div class="clearfix sureChoose">
            <mu-button class="chooseBtn fll" @click="handleRemove">清空</mu-button>
            <mu-button class="chooseBtn flr sure" @click="handleSure">确定</mu-button>
        </div>
    </div>

</template>

<script>
    export default {
        data() {
            return {
                isShow: false,
                isShow1: false,
                isShow2: false,
                isShow3: false,
                isActive3: 0,
                isActive2: 0,
                isActive: 0,
                result:[]   ,
                financingMoneyList: [],
                financingWayList: [],
                industryList: [],
                regionList: []

            };
        },
        methods: {
            handleShowList() {
                this.isShow = true

            },
            handleCloseList() {
                this.isShow = false
            },
            handleShowList1() {
                this.isShow1 = true

            },
            handleCloseList1() {
                this.isShow1 = false
            },
            handleShowList2() {
                this.isShow2 = true

            },
            handleCloseList2() {
                this.isShow2 = false
            },
            handleShowList3() {
                this.isShow3 = true

            },
            handleCloseList3() {
                this.isShow3 = false
            },
            checkItem(index) {
                this.isActive = index

            },
            checkItem1(index) {
                this.type[index].like = !this.type[index].like;
            },
            checkItem2(index) {
                // this.label[index].like = !this.label[index].like;
                this.isActive2 = index
            },
            checkItem3(index) {
                this.isActive3 = index
            },
            // likeAll() {
            //     this.label.forEach(item => {
            //     item.like = 1;
            // });}
            getType() {
                this.$axios.get(`/jsp/wap/trProject/ctrl/jsonCategoryList.jsp`).then(res => {
                    console.log("项目分类", res)
                    if (res.success == "true") {
                        this.financingMoneyList = res.data.financingMoneyList
                        this.financingWayList = res.data.financingWayList
                        this.industryList = res.data.industryList
                        this.regionList = res.data.regionList
                    }
                })
            },
            handleRemove(){

            },
            handleSure(){

            }
        },
        created() {
            this.getType()
        }

    };
</script>
<style scoped lang="scss">
    .chooseBox {
        background: #fff;
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

    .type .checkBtn {
        width: 1.6rem;
        text-align: center;
        padding: .1rem .15rem;
        border-radius: 10%;
        margin-right: .2rem;
        margin-top: .2rem;
        font-size: .24rem;
        font-family: "PingFang";
        cursor: pointer;

    }
    .type input{
        display: none
    }

    .radioItem {
        background: #eee;
        color: rgb( 102, 102, 102);
        width: 1.6rem;
        text-align: center;
        padding: .1rem .15rem;
        border-radius: 10%;
        margin-right: .2rem;
        margin-top: .2rem;
        font-size: .24rem;
        font-family: "PingFang";

    }

    .active {
        background: #005982;
        color: #fff
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

    #moneyType {
        width: 2rem
    }

    .like {
        background: #005982;
        color: #fff;
    }

    .nolike {
        background: #eee;
        color: rgb( 102, 102, 102);
    }
</style>