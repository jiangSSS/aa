<template>

    <div class="all" :data="projectDetail">
        <Header></Header>
        <div class="containerAll">
            <div class="detail">
                <div class="projectHeader">
                    <div class="projectTitle">{{projectDetail.title}}</div>
                    <div class="time">
                        <span>编号：</span>
                        <span>{{projectDetail.projectId}}</span>
                    </div>
                    <div class="clearfix">
                        <div class="fll time">
                            <i class="iconfont icon-shijian"></i>
                            <span>{{projectDetail.addTimeStr}}</span>
                        </div>
                        <div class="sendBtn flr isFollow" v-if="follow" @click="isFollow">已关注</div>
                        <div class="sendBtn flr likeBtn" v-else @click="noFollow">关注</div>
                        <div class="sendBtn flr" @click="handleTell">我要约谈</div>
                    </div>
                    <mu-dialog width="400" center class="applyDialog" :open.sync="isShowApply">
                        <select class="oneRows" v-model="moneyId">
                            <option :value="item.id" v-for="item in myMoney" :key="item.index" :label="item.title">{{item.title}}</option>
                        </select>
                        <div class="btnSend">
                            <mu-button class="applyBtn" @click="closeApply">确认</mu-button>
                            <mu-button class="applyBtn" @click="isShowApply = false">取消</mu-button>
                        </div>
                    </mu-dialog>

                </div>
                <div class="user clearfix" @click="$router.push({name:'projectInvestors',query:{id}})">
                    <img class="fll" src="../../../static/app/img/usrname.jpg" style="width:1rem">
                    <span class="fll">李先生</span>
                    <div class="flr">
                        <span class="">北京开拓明天有限公司</span>
                        <i class="iconfont icon-xiangyou"></i>
                    </div>
                </div>
                <!-- <div class="user clearfix">
                    <div class="fll titleDesc">融资信息</div>
                    <div class="flr customer">
                        客户要求保密
                    </div>

                </div> -->
                <div class="message">
                    <div>
                        <span>融资主体:</span>
                        <span>{{projectDetail.financeBodyName}}</span>
                    </div>
                    <div>
                        <span>所在地区:</span>
                        <span>{{projectDetail.regionNameStr}}</span>

                    </div>
                    <div>
                        <span>公司估值:</span>
                        <span>{{projectDetail.companyAssessed}}</span>

                    </div>
                    <div>
                        <span>市净率(P/B):</span>
                        <span>{{projectDetail.pb}}</span>

                    </div>
                    <div>
                        <span>市盈率(P/E):</span>
                        <span>{{projectDetail.pe}}</span>

                    </div>
                    <div>
                        <span>行业性质:</span>
                        <span>{{projectDetail.industryName}}</span>

                    </div>
                    <div>
                        <span>支付方式:</span>
                        <span>{{projectDetail.paymentTypeName}}</span>

                    </div>
                    <div>
                        <span>融资用途:</span>
                        <span>{{projectDetail.financingExplain}}</span>

                    </div>
                    <div>
                        <span>融资金额:</span>
                        <span>{{projectDetail.paymentTypeName}}</span>

                    </div>
                    <div>
                        <span>总投资额:</span>
                        <span>{{projectDetail.investIndustryName}}</span>

                    </div>
                    <div>
                        <span>意向资金: </span>
                        <span>{{projectDetail.intentCapitalList}}</span>

                    </div>
                    <div>
                        <span>投资方式:</span>
                        <span>{{projectDetail.financingWayName}}</span>

                    </div>
                </div>
                <div class="user clearfix" @click="$router.push('/money/progress')">
                    <div class="fll">查看项目进展</div>
                    <div class="flr">
                        <i class="iconfont icon-xiangyou"></i>
                    </div>
                </div>
                <div class="contentTell">
                    <div class="detaila">
                        <div class="peojectTitle">项目介绍</div>

                    </div>
                    <div class="contentDesc">{{projectDetail.brief}}</div>
                    <div>
                        <img src="/static/app/img/detailImg1.jpg" alt="">
                    </div>
                </div>
                <div class="contentTell">
                    <div class="detaila">
                        <div class="peojectTitle">核心团队</div>
                    </div>
                        <div class="coreDetail">
                            {{projectDetail.teamBrief}}
                        </div>
                    </div>
                </div>
                <div class="contentTell">
                    <div class="detaila">
                        <div class="peojectTitle">项目点评</div>

                    </div>
                    <div class="" v-for="(item,index) in review" :key="index">
                        <div class="coreName">
                            {{item.title}}
                        </div>
                        <div class="coreDetail">
                            {{item.desc}}
                        </div>
                    </div>
                </div>
                <div class="contentTell ">
                    <div class="detaila">
                        <div class="peojectTitle">可能感兴趣的项目</div>
                    </div>
                    <div class="mayProject" v-for="(item,index) in mayProject" :key="index">
                        <div class="mayTitle">
                            {{item.title}}
                        </div>
                        <div class="mayTime">
                            <i class="iconfont icon-shijian"></i>
                            <span>{{item.time}}</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- <Footer class="footer"></Footer> -->
    </div>
</template>

<script>
    import Header from "@/components/Header.vue"
    import Footer from "@/components/Bottom.vue"
    import { Dialog } from 'vant';
    // import commentDetailVue from '../activity/commentDetail.vue';
    import { Toast } from 'mint-ui'
    import * as Cookies from 'js-cookie'
    export default {
        components: {
            Header,
            Footer,
            Toast
        },
        data() {
            return {
                core: [
                    {
                        name: "张麟（法人）",
                        detail: "之前就职于苏州工业园区大型企业10多年，管理企业大型项目，对现代化企业管理流程熟悉。"
                    },
                    {
                        name: "黄羽（总经理）",
                        detail: "之前就职于苏州工业园区大型企业10多年，管理企业大型项目，对现代化企业管理流程熟悉。"
                    },
                ],
                review: [
                    {
                        title: "完整的逻辑架构",
                        desc: "打造符合投资人口味的完整计划书逻辑框架和商业模式，提出优化建议。"
                    },
                    {
                        title: "清晰的商业模式",
                        desc: "打造符合投资人口味的完整计划书逻辑框架和商业模式，提出优化建议。"
                    },
                ],
                mayProject: [
                    {
                        title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                        time: "2018-01-01"
                    },
                    {
                        title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                        time: "2018-01-01"
                    },
                    {
                        title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                        time: "2018-01-01"
                    },
                    {
                        title: "预防近视阻止近视发生发展的可穿戴品，健康医疗领域，需要融资项目，金额为100万元",
                        time: "2018-01-01"
                    },
                ],
                projectDetail: [],
                follow: 0,
                id: "",

                isShowApply: false,
                myMoney: [],
                projectId: "",
                moneyId: "",
                myMoney_Count: 0,
            }
        },
        methods: {

            getMyMoney(pn) {
                this.$axios.get("/jsp/wap/center/ctrl/jsonIssueCapitalList.jsp", {
                    params: { pageNumber: pn }
                }).then(res => {
                    this.myMoney = res.data.pageList;
                    var myMoney = res.data.pageList
                    if (myMoney.length > 0) {
                        this.moneyId = myMoney[0].id
                    }
                    this.myMoney_Count = Number(res.data.pagination.totalCount);
                });
            },
            // 约见项目方
            handleTell(id) {
                if (Cookies.get("userKey")) {
                    if (this.myMoney.length == 0) {
                        let instance = Toast('您还没有发布资金，请先发布资金');
                        setTimeout(() => {
                            instance.close();
                        }, 2000);
                    } else {
                        this.isShowApply = true;
                        this.projectId = this.$route.query.id;
                    }
                }
                else {
                    let instance = Toast('您还未登录，请先登录');
                    setTimeout(() => {
                        instance.close();
                    }, 2000);
                }
            },
            // 确认投递 关闭投递框
            closeApply() {
                this.$axios.get("/jsp/wap/trCapital/do/doDeliver.jsp", {
                    params: { id: this.moneyId, projectId: this.projectId }
                })
                    .then(res => {
                        if (res.success == "true") {
                            let instance = Toast('提交成功，平台将尽快为您安排');
                            setTimeout(() => {
                                instance.close();
                            }, 2000);
                        } else {
                            let instance = Toast(res.message);
                            setTimeout(() => {
                                instance.close();
                            }, 2000);
                        }
                    });
                setTimeout(() => {
                    this.isShowApply = false;
                }, 500);
            },

            // 模态框
            // handleTell() {
            //     Dialog.alert({
            //         img: "/static/app/img/success.jpg",
            //         title: "提交成功",
            //         message: '平台会尽快为你安排。'
            //     }).then(() => {
            //         // on close
            //     });
            // },
            // 获取项目详情
            getProjectDetail() {
                this.id = this.$route.query.id
                this.$axios.get(`/jsp/wap/trProject/ctrl/jsonProjectDetail.jsp?id=${this.id}`, ).then(res => {
                    console.log("项目详情", res)
                    this.projectDetail = res.data.project   
                })
            },
            // 获取关注状态
            getFollow() {
                this.$axios.get(`/jsp/wap/trProject/ctrl/jsonIsFollow.jsp?id=${this.id}`).then(res => {
                    // this.follow 
                    console.log("是否关注", res)
                    this.follow = Number(res.data)
                })
            },
            // 关注
            noFollow() {
                this.$axios.get(`/jsp/wap/trProject/do/doFollow.jsp?id=${this.id}`).then(res => {
                    console.log("关注", res)
                    if (res.success == "true") {
                        let instance = Toast('关注成功');
                        setTimeout(() => {
                            instance.close();
                        }, 1000);
                        this.follow = 1
                    } else {
                        let instance = Toast('关注失败，请检查登录状态');
                        setTimeout(() => {
                            instance.close();
                        }, 1000);
                    }
                })
            },
            // 取消关注
            isFollow() {
                this.$axios.get(`/jsp/wap/trProject/do/doUnfollow.jsp?id=${this.id}`).then(res => {
                    console.log("取消关注", res)
                    if (res.success == "true") {
                        let instance = Toast('已取消关注');
                        setTimeout(() => {
                            instance.close();
                        }, 1000);
                        this.follow = 0
                    } else {
                        let instance = Toast('取消失败');
                        setTimeout(() => {
                            instance.close();
                        }, 1000);
                    }
                })
            },
            // 项目进展
            getProgress() {
                this.$axios.get(`/jsp/wap/trProject/ctrl/jsonProjectDynamicList.jsp?id=${this.id}`).then(res => {
                    console.log("项目进展", res)
                })
            }

        },
        created() {
            this.getProjectDetail()
            this.getFollow()
            this.getProgress()/*  */
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    .containerAll {
        background: #f3f5f7; // margin-bottom: 1rem
    }

    img {
        width: 100%
    }

    .detail {
        background: #f3f5f7;
    }

    .projectTitle {
        font-size: .3rem;
        font-family: "PingFang";
        color: rgb( 51, 51, 51);
        font-weight: bold;
        line-height: 1.6;
        padding: .3rem 0 0 0;
    }

    .sendBtn {
        border: 1px solid #005982;
        border-radius: 2px;
        display: inline-block;
        color: #005982;
        padding: .1rem;
        height: .6rem;
        width: 1.2rem;
        line-height: .4rem;
        font-family: "PingFang";
        font-size: .23rem;
        font-weight: bold;
        opacity: 1;
        margin-right: .3rem;
        text-align: center;
    }

    .likeBtn {
        // color: #ccc;
        // border: 1px solid #ccc;
    }

    .isFollow {
        color: #fff;
        background: #005982
    }

    .time {

        font-size: .3rem;
        font-family: "PingFang";
        color: rgb(137, 137, 137);
        line-height: 2;

    }

    .projectHeader {
        background: #fff;
        padding: .8rem .2rem .1rem;
        margin-bottom: .3rem
    }

    .user {
        line-height: 3;
        padding: .2rem;
        background: #fff;
        margin-bottom: .3rem
    }

    .titleDesc {
        font-size: .3rem;
        color: rgb( 51, 51, 51);
    }

    .customer {
        color: rgb( 0, 89, 130);
    }

    .contentTell {
        background: #fff;
        padding: .2rem;
        margin-bottom: .3rem;
        .detaila {
            background: #fff;
            padding: .2rem 0;
            border-bottom: 1px solid #f3f5f7;
            .peojectTitle {
                border-left: 3px solid #005982; // margin: 0 .3rem;
                padding-left: .2rem;
                font-size: .3rem;
                font-family: "PingFang";
                color: rgb( 51, 51, 51);
                line-height: 1.533;


            }
        }
        .contentDesc {
            color: rgb(128, 128, 128);
            padding: .1rem 0;
            line-height: 1.5;
        }
    }

    .coreDetail {
        color: rgb(128, 128, 128);
    }

    .coreName {
        font-weight: 700;
        padding: .2rem 0 0;
    }

    .mayProject {
        padding: .1rem 0;

    }

    .mayTitle {
        color: rgb(128, 128, 128);
    }

    .mayTime {
        line-height: 2;
        color: rgb(128, 128, 128);
    }

    .message {
        background: #fff;
        padding: .2rem;
        margin-bottom: .3rem
    }

    .message div {
        line-height: 2
    }

    .message div span:nth-child(1) {
        font-family: "PingFang";
        color: rgb(137, 137, 137);
        display: inline-block;
        margin-right: .1rem
    }

    /*  */
    .applyBtn {
        /* width: 90%; */
        background: #005982;
        color: #fff;
        margin-top: 0.4rem;
    }
    .btnSend{
        text-align: center;
    }
    /deep/ .mu-dialog-body{
        padding: .7rem .5rem .5rem
    }

    .oneRows {
        width: 4.6rem
    }
</style>