<template>
    <div class="all">
        <Header></Header>
        <div class="containerAll">
            <div class="detail">
                <div class="headerWarp">
                    <div class="title">开拓绿色能源自主创新之路</div>
                    <div class="clearfix">
                        <div class="fll">
                            <span>作者：</span><span>张璐 何牧文</span><span>(来源：<span>天津日报</span> )</span>
                        </div>
                        <div class="flr"><span>2019-01-09 15:14:58</span></div>             
                    </div>
                </div>
                <div>
                    <div class="contentImg">
                        <img src="http://39.96.39.111:6022/upload/45/45c3441d9485f25c333ca2d4d607cae8/file.jpg" alt="">
                    </div>
                    <div class="contentText">
                    <p style="text-align: left; text-indent: 2em;">在8日召开的国家科学技术奖励大会上，南开大学化学学院陈永胜教授领衔完成的“面向能源转化与存储的有机和碳纳米材料研究”项目荣获国家自然科学奖二等奖。接受采访时陈永胜表示：“作为世界各国在新能源研究中竞争最为激烈的领域之一，开发并引领具有独立的自主知识产权的有机太阳能电池材料和技术，为我国赢得先机，一直是这一领域内中国科学家的努力方向。”</p> 
                        </div>    
                </div>
            </div>
        </div>
        <div class="footer">
            <div>
                <i class="iconfont icon-dianzan"></i>
                <span>60</span>
            </div>
            <div @click="$router.push('/activityDetail/comment')">
                <i class="iconfont icon-weibiaoti-"></i>
                <span>60</span>
            </div>
            <div>
                <i class="iconfont icon-share"></i>
                <span>分享</span>
            </div>
        </div>
        <!-- <div class="apply" @click="handleApply">
            <i class="iconfont icon-bianji1"></i>
            <span>报名</span>
        </div> -->
        <mu-dialog width="400" center class="applyDialog" :open.sync="openSimple">
            <p class="dialogTitle">报名信息</p>
            <div class="">
                <i class="iconfont icon-My"></i>
                <input class="" type="text" placeholder="请输入姓名">
            </div>
            <div>
                <i class="iconfont icon-shouji"></i>
                <input type="text" placeholder="请输入手机号">

            </div>
            <div>
                <i class="iconfont icon-neirong"></i>
                <input type="text" placeholder="请输入内容">

            </div>
            <mu-button class="applyBtn" @click="closeApply">确认</mu-button>
        </mu-dialog>
    </div>
</template>

<script>
    import Header from "@/components/Header.vue"
    import Footer from "@/components/Bottom.vue"

    export default {
        components: {
            Header,
            Footer
        },
        data() {
            return {
                // newsDetail:[],
                // core: [
                //     {
                //         name: "张麟（法人）",
                //         detail: "之前就职于苏州工业园区大型企业10多年，管理企业大型项目，对现代化企业管理流程熟悉。"
                //     },
                //     {
                //         name: "黄羽（总经理）",
                //         detail: "之前就职于苏州工业园区大型企业10多年，管理企业大型项目，对现代化企业管理流程熟悉。"
                //     },
                // ],
                // review: [
                //     {
                //         title: "完整的逻辑架构",
                //         desc: "打造符合投资人口味的完整计划书逻辑框架和商业模式，提出优化建议。"
                //     },
                //     {
                //         title: "清晰的商业模式",
                //         desc: "打造符合投资人口味的完整计划书逻辑框架和商业模式，提出优化建议。"
                //     },
                // ],
                // mayProject: [
                //     {
                //         title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                //         time: "2018-01-01"
                //     },
                //     {
                //         title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                //         time: "2018-01-01"
                //     },
                //     {
                //         title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                //         time: "2018-01-01"
                //     },
                //     {
                //         title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                //         time: "2018-01-01"
                //     },
                // ],
                openSimple: false,
                // widthDialog:"3rem"
            }
        },
        methods: {
            handleApply() {
                this.openSimple = true;
            },
            closeApply() {
                this.openSimple = false;
            },
            // getNewsDetail(){
            //     let id = this.$route.query.id
            //     this.$axios.get(`/jsp/wap/trNews/ctrl/jsonNewsDetail.jsp?id=${id}`).then(res=>{
            //         console.log("新闻详情",res)
            //         this.newsDetail = res.data
            //     })
            // }
        },
        // created(){
        //     this.getNewsDetail()
        // }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    .containerAll {
        background: #f3f5f7;
        margin-bottom: 1rem
    }

    img {
        width: 100%
    }

    .detail {
        background: #fff;
        padding: 1rem .3rem 0;
    }

    .title {
        font-size: .32rem;
        font-family: "PingFang";
        color: rgb( 51, 51, 51);
        font-weight: bold;
        line-height: 2;
    }

    .headerWarp {
        padding-bottom: .2rem
    }

    .headerWarp span {
        font-size: .24rem;
        font-family: "PingFang";
        color: rgb( 153, 153, 153);
        line-height: 2;
    }

    .contentText {
        font-size: .3rem;
        font-family: "PingFang";
        color: rgb( 102, 102, 102);
        line-height: 1.429;
    }

    .contentImg {
        padding: .3rem 0
    }

    .footer {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        background-size: 100%;
        display: flex;
        background: #fff;
        div {
            width: 2.5rem;
            flex: 1;
            text-align: center;
            span {
                font-size: .32rem;
                font-family: "PingFang";
                color: rgb( 102, 102, 102);
                line-height: 2.5;
                margin-left: .1rem
            }
        }
    }
    .icon-dianzan,
    .icon-weibiaoti-,
    .icon-share {
        font-size: .4rem
    }

    .applyDialog {
        text-align: center;
        margin: 0 auto;
        input {
            border: 0;
            border-bottom: 1px solid rgb(237, 237, 237);
            line-height: 2.6;
            margin-left: .1rem;
            width: 80%;
        }
        .iconfont {
            font-size: .6rem; // padding-top: 1rem;
            display: inline-block
        }
    }

    .dialogTitle {
        font-weight: bold;
        font-size: .34rem
    }

    .applyBtn {
        width: 90%;
        background: #005982;
        color: #fff;
        text-align: center;
        margin-top: .4rem
    }
</style>