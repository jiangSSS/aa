<template>
    <div class="all">
        <div class="header">
            <div class="searchBox" @click="$router.push('/searchList')">
                <i class="iconfont icon-sousuo"></i>
            </div>
            <div class="logoBox">
                <img src="../../../static/app/img/home/logo.png" class="logo">
            </div>
            <div class="rightBox" @click="tokefu">
                <img src="../../../static/app/img/home/header_right.jpg" class="header_right">
            </div>
        </div>

        <div class="detail">
            <div class="swiper">
                <swiper :options="swiperOption">
                    <swiper-slide v-for="(item,index) in banner" :key="index">
                        <!-- <router-link :to="{name:'newsDetail',params:{id:item.url}}"> -->
                        <div>
                            <img :src="$url + item.appImgPath">
                            <!-- <span class="swiper-title">{{item.title}}</span> -->
                        </div>
                        <!-- </router-link> -->
                    </swiper-slide>
                    <div class="swiper-pagination" slot="pagination"></div>
                    <!-- <div class="swiper-button-prev" slot="button-prev">  </div>
                    <div class="swiper-button-next" slot="button-next">  </div> -->
                </swiper>
            </div>
            <div class="tab">
                <router-link to="/money">
                    <div>
                        <div>
                            <img src="../../../static/app/img/home/0a.jpg" alt="">
                        </div>
                        <div class="title">资金</div>
                    </div>
                </router-link>
                <router-link to="/projectA">
                    <div>
                        <div>
                            <img src="../../../static/app/img/home/0b.jpg" alt="">
                        </div>
                        <div class="title">项目</div>
                    </div>
                </router-link>
                <router-link to="/activity">
                    <div>
                        <div>
                            <img src="../../../static/app/img/home/0c.jpg" alt="">
                        </div>
                        <div class="title">活动会议</div>
                    </div>
                </router-link>
                <router-link to="/news">
                    <div>
                        <div>
                            <img src="../../../static/app/img/home/0d.jpg" alt="">
                        </div>
                        <div class="title">资讯</div>
                    </div>
                </router-link>
            </div>
            <div class="clearfix">
                <img src="../../../static/app/img/home/homeContent1.jpg" class="homeContent1 fll">
                <div class="fll contentRight1">
                    <p class="row1">会员周报</p>
                    <div class="row2">
                        <span>2018年第二期 </span>
                        <span @click="$router.push('/weekDetail')"> 点击阅读</span>
                    </div>
                </div>
            </div>
            <div class="issue">
                <router-link to="/issueMoney">
                    <img src="../../../static/app/img/home/c1.png" alt="">
                </router-link>
                <router-link to="/issueProject">
                    <img src="../../../static/app/img/home/c2.png" alt="">
                </router-link>
                <router-link to="/demand">
                    <img src="../../../static/app/img/home/c3.png" alt="">
                </router-link>

            </div>

            <div>
                <img src="../../../static/app/img/home/contentImg2.jpg" alt="">
            </div>
            <div class="subtitle">
                <span class="titleContent" @click="$router.push('/projectA')">优质项目
                    <i class="iconfont icon-xiangyou"></i>
                </span>
            </div>
            <div v-for="(item,index) in projectList.slice(0,2)" :key="index" class="wellProject">
                <router-link :to="{path:'/projectA/projectDetail',query:{id:item.id}}">
                    <img :src="$url + item.recommendImgPath" alt="" class="wellImg">
                    <div class="wellTitle">
                        {{item.title}}
                    </div>
                    <div class="wellCompany">{{item.companyName}}</div>
                    <div class="wellContent">{{item.brief}}</div>
                </router-link>

            </div>
            <div class="moneyBoxa">
                <div class="subtitle">
                    <span class="titleContent" @click="$router.push('/money')">优质资金
                        <i class="iconfont icon-xiangyou"></i>
                    </span>
                </div>
                <div class=" moneyBox" v-for="item in capitalList.slice(0,2)" :key="item.index">
                    <router-link :to="{path:'/money/moneydetail',query:{id:item.id}}" class="clearfix">
                        <div class="flr imgBox">
                            <img :src="$url + item.recommendImgPath" class="wellMoney"> </div>
                        <div class="fll rightContent">
                            <div class="rightTitle">{{item.title}}</div>
                            <div class="rightList">
                                <div>
                                    <span>投资资金:</span>
                                    <span class="moneyNum">{{item.investAmountName}}</span>
                                </div>
                                <div>
                                    <span>投资方式:</span>
                                    <span>{{item.investCase}}</span>
                                </div>
                                <div>
                                    <span>投资类型:</span>
                                    <span>{{item.investTypeName}}</span>
                                </div>
                                <div>
                                    <span>资金来源:</span>
                                    <span>{{item.capitalSourceName}}</span>
                                </div>
                                <div>
                                    <span>资金类型:</span>
                                    <span>{{item.capitalType}}</span>
                                </div>
                                <div>
                                    <span>投资行业:</span>
                                    <span>{{item.investWayName}}</span>
                                </div>
                            </div>
                        </div>
                    </router-link>
                </div>
            </div>
            <div class="subtitle">
                <span class="titleContent" @click="$router.push('/news')">投融资讯
                    <i class="iconfont icon-xiangyou"></i>
                </span>
            </div>
            <div v-for="item in pageList.slice(0,4)" :key="item.index">
                <router-link :to="{path:'/newsDetail',query:{id:item.id}}">
                    <div class="clearfix rows">
                        <div class="nums clearfix flr">
                            <div class="clearfix titleBox">
                                <img src="../../../static/app/img/my/dian.jpg" class="dian fll">
                                <span class="fll messageTitle">{{item.title}}</span>
                            </div>
                            <div class="messageTime">
                                <span class="fll timestatus">{{item.addTimeStr.slice(0,10)}}</span>
                                <span class="flr rightTime">
                                    <span>(来源：
                                        <span>{{item.source}}</span> )</span>
                                </span>
                            </div>
                            <div class="newsDesc">
                                {{item.brief}}
                            </div>
                        </div>
                        <div class="newsImgBox fll">
                            <img :src="$url + item.imgPath" class="newsImg">
                        </div>
                    </div>
                </router-link>
            </div>
            <p class="noData">--- 没有数据了 ---</p>
        </div>
        <Footer class="footer"></Footer>
    </div>
</template>
<script>
    import Footer from "@/components/Bottom.vue";
    import "swiper/dist/css/swiper.css";
    import { swiper, swiperSlide } from "vue-awesome-swiper";
    export default {
        components: {
            Footer,
            swiper,
            swiperSlide
        },
        data() {
            return {
                banner: [],
                projectList: [],
                capitalList: [],
                swiperOption: {
                    // 显示分页
                    pagination: {
                        el: ".swiper-pagination",
                        clickable: true
                    },
                    waitForTransition: true,
                    // 设置自动播放速度
                    autoplay: {
                        disableOnInteraction: false,
                        delay: 2000
                    },
                    // 开启无限循环
                    loop: false,
                    //设置点击箭头
                    paginationClickable: true,
                    prevButton: ".swiper-button-prev",
                    nextButton: ".swiper-button-next",
                    //设置同屏显示的数量，默认为1，使用auto是随意的意思。
                    slidesPerView: 1,
                    //开启鼠标滚轮控制Swiper切换。可设置鼠标选项，或true使用默认值。
                    mousewheel: false
                    //默认为false，普通模式：slide滑动时只滑动一格，并自动贴合wrapper，设置为true则变为free模式，slide会根据惯性滑动可能不止一格且不会贴合。
                    // freeMode:true
                },
                pageList: [],
                messageList: [
                    {
                        title:
                            "开拓绿色能源自主创新之路开拓绿色能源自主创新之路开拓绿色能源自主创新之路开拓绿色能源自主创新之路开拓绿色能源自主创新之路开拓绿色能源自主创新之路'",
                        time: "2019-11-11"
                    },
                    {
                        title: "开拓绿色能源自主创新之路开拓绿色能源自主创新之路'",
                        time: "2018-11-11"
                    },
                    {
                        title: "开拓绿色能源自主创新之路开拓绿色能源自主创新之路'",
                        time: "2017-11-11"
                    }
                ]
            };
        },
        methods: {
            getSwiper() {
                this.$axios.get(`/jsp/wap/index/ctrl/jsonIndex.jsp`).then(res => {
                    console.log("轮播图", res);
                    this.banner = res.data.banner;
                    this.capitalList = res.data.capitalList;
                    this.projectList = res.data.projectList;
                });
            },
            tokefu() {
                window.open("https://tb.53kf.com/code/app/10193554/1", "_blank");
            },
            getNewsList() {
                this.$axios.get(`/jsp/wap/trNews/ctrl/jsonNewsPage.jsp`).then(res => {
                    console.log("新闻列表", res);
                    if (res.success == "true") {
                        this.pageList = res.data.pageList;
                    }
                });
            }
        },
        created() {
            this.getNewsList();
            this.getSwiper();
        }
    };
</script>

<style scoped lang="scss">
    // 头部
    .all {
        position: relative;
        width: 100%;
    }

    .newsImg {
        width: 2rem;
    }

    .aaaa {
        width: 4.5rem;
        color: #333 !important;
    }

    .titleImg {
        font-size: 0.24rem;
        color: #ccc;
    }

    .timedata {
        margin-left: 0.4rem;
    }

    .threes {
        display: flex;
        justify-content: space-between;
    }

    .threes img {
        width: 2rem;
        height: 1.6rem;
    }

    .header {
        display: flex;
        justify-content: space-between;
        padding: 0.15rem;
        height: 1rem; // position: fixed;
        background: #fff;
        top: 0;
        .logo {
            width: 2.2rem;
        }
        .logoBox {
            line-height: 2.5;
            margin-top: 0.1rem;
        }
        .rightBox {
            line-height: 2;
        }
        .header_right {
            width: 0.45rem;
            text-align: center;
            margin-top: 0.1rem;
            margin-right: 0.2rem;
        }
        .search {
            font-size: 0.3rem;
            display: block;
            padding-top: -0.1rem;
        }
        .searchBox {
            margin-left: 0.1rem;
            text-align: center;
            .iconfont {
                font-size: 0.5rem;
            }
        }
    }

    .detail {
        padding-bottom: 1.4rem;
    }

    .noData {
        text-align: center;
        color: #999;
    } //  轮播图
    .swiper {
        img {
            height: 3.75rem;
            width: 7.5rem;
            display: block;
        }
    }

    img {
        width: 100%;
    } // tab卡
    .tab {
        display: flex;
        justify-content: space-around;
        padding: 0.3rem 0.4rem;
        text-align: center;

        img {
            width: 0.7rem;
        }
        a {
            color: rgba(0, 0, 0, 0.8);
        }
        .title {
            font-size: 0.25rem; // display: inline-block;
            margin-top: -0.05rem;
        }
    } // content
    .homeContent1 {
        width: 50%;
        vertical-align: text-top;
    }

    .contentRight1 {
        padding-left: 0.3rem;
        padding-top: 0.8rem;
    }

    .row1 {
        font-weight: 700;
        font-size: 0.4rem;
        padding: 0;
        margin: 0;
    }

    .row2 {
        margin-bottom: 0.2rem;
        padding: 0 !important;
        span:nth-child(1) {
            padding-right: 0.1rem;
            font-size: 0.28rem;
        }
        span:nth-child(2) {
            color: #005982;
            font-weight: 700;
            font-size: 0.28rem;
        }
    }

    .subtitle {
        padding: 0.3rem;
        text-align: center;
        margin: 0 auto;
    }

    .titleContent {
        font-size: 0.4rem;
        line-height: 3;
        font-family: "MicrosoftYaHeiLight";
        color: rgb(137, 137, 137);
        line-height: 1.333;  
    }

    .icon-xiangyou {
        background: rgb(230, 230, 230);
        padding: .04rem;
        margin-left: 0.2rem;
    }

    .wellProject {
        padding: 0.2rem 0.3rem;
        .wellTitle {
            font-size: 0.3rem;
            font-family: "Microsoft YaHei";
            color: rgb(62, 58, 57);
            font-weight: bold;
            line-height: 1.5;
        }
        .wellCompany {
            font-size: 0.18rem;
            font-family: "Microsoft YaHei";
            color: rgb(62, 58, 57);
            line-height: 1.5;
            padding-bottom: 0.2rem;
        }
        .wellImg {
            width: 100%;
            // height: 3rem;
        }
        .wellContent {
            font-size: 0.24rem;
            font-family: "Microsoft YaHei";
            color: rgb(137, 137, 137);
            line-height: 1.429;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical !important;
        }
    }

    .wellMoney {
        width: 100%;
        height: 100%;
    }

    .imgBox {
        width: 50%;
        height: 4.2rem;
    }

    .moneyBox:nth-child(even) {
        .rightContent {
            float: right;
        }
        .imgBox {
            float: left;
        }
    }

    .rightContent {
        width: 50%;
        padding: 0.2rem;
        img {
            vertical-align: middle;
        }
        .rightTitle {
            font-size: 0.3rem;
            font-family: "Microsoft YaHei";
            color: rgb(62, 58, 57);
            font-weight: bold;
            padding-bottom: 0.1rem; // margin-bottom: .1rem;
            overflow: hidden;
            height: 0.9rem;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical !important;
        }
        .moneyNum {
            color: #005982;
            font-size: 0.26rem !important;
            font-weight: bold;
        }
    }

    .rightList div {
        clear: both;
        line-height: 2;
    }

    .rightList span:nth-child(1) {
        font-family: "PingFang";
        color: #999; // display: inline-block;
        font-size: 0.24rem;
        float: left;
    }

    .rightList span:nth-child(2) {
        float: left;
        font-size: 0.24rem;
        color: #333; // display: inline-block;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        width: 2.2rem;
    }

    .dian {
        margin: 0.15rem;
    }

    .moneyBoxa {
        background: #fafafa;
    }

    .rows {
        padding: 0.1rem 0.3rem;
        border-bottom: 0.2rem solid #fafafa;
        .messageTitle {
            font-size: 0.24rem;
            font-family: "Microsoft YaHei";
            color: rgb(51, 51, 51);
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            width: 80%;
            // line-height: 2;
        }
        .messageTime {
            font-size: 0.2rem;
            font-family: "Microsoft YaHei";
            color: rgb(137, 137, 137);
            line-height: 2;
        }
        .messageTime span {
            font-size: 0.2rem;
        }
        .timestatus {
            margin-left: 0.3rem;
        }
        .rightTime {
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
            width: 2.4rem;
        }
    }
    .titleBox{
        margin-top: .15rem
    }

    .dian {
        margin: 0.15rem;
    }

    .newsImgBox {
        // display: flex;
        // justify-content: space-between;
        padding-top: 0.15rem;
        .newsImg {
            width: 2.2rem;
            height: 2rem;
        }
    }

    .nums {
        width: 4.5rem;
    }

    .newsDesc {
        color: #666;
        float: right;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        width: 4.2rem;
        font-size: 0.24rem;
        margin-top: 0.1rem;
    }
    .issue{
        display: flex;
        justify-content: space-around
    }

    .issue img{
        vertical-align: middle
    }
    .titleBox{
        margin-top: .15rem
    }
</style>