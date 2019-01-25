<template>

    <div class="all" :data="activityDetail">
        <Header></Header>
        <div class="containerAll">
            <div class="detail">
                <div class="headerWarp">
                    <div class="title">{{activityDetail.title}}</div>
                    <div>
                        <span>主办：</span>
                        <span>{{activityDetail.speaker}}</span>
                    </div>
                    <div>
                        <span>地点：</span>
                        <span>{{activityDetail.address}}</span>
                    </div>
                    <div>
                        <span>活动时间：</span>
                        <span>{{activityDetail.regStartTimeStr}}</span>
                        <span>至</span>
                        <span>{{activityDetail.regEndTimeStr}}</span>
                    </div>
                </div>
                <div>
                    <div class="contentImg">
                        <img :src="$url + activityDetail.imgPath" class="detailImg" alt="">
                    </div>
                    <div class="contentText" v-html="activityDetail.content"></div>
                </div>
            </div>
        </div>
        <div class="footer">
            <div v-if="good" @click="isGood">
                <i class="iconfont icon-dianzan" style="color:#f00"></i>
                <span>{{activityDetail.greatNum}}</span>
            </div>
            <div v-else @click="noGood">
                <i class="iconfont icon-dianzan"></i>
                <span>{{activityDetail.greatNum}}</span>
            </div>
            <div @click="$router.push({name:'activityComments',query:{id}})">
                <i class="iconfont icon-weibiaoti-"></i>
                <span>{{countComment}}</span>
            </div>
            <div @click="share = true">
                <i class="iconfont icon-share"></i>
                <span>分享</span>
            </div>

        </div>
        <van-popup v-model="share" position="bottom" :overlay="true" class="shareBox">
            <!-- <van-area :area-list="areaList" @cancel="onCancel" @confirm="onConfirm" @change="onChange"></van-area> -->
            <share :config="config"></share>
            <div class="cancelShare" @click="share = false">取消</div>
        </van-popup>
        <div class="apply" @click="isShowApply = true" v-show="activityDetail.status == 1">
            <i class="iconfont icon-bianji1"></i>
            <span>报名</span>
        </div>
        <div class="apply end" v-show="activityDetail.status == 0">
            <i class="iconfont icon-bianji1"></i>
            <span>尚未开始</span>
        </div>
        <div class="apply end" v-show="activityDetail.status == -1">
            <i class="iconfont icon-bianji1"></i>
            <span>往期回顾</span>
        </div>
        <mu-dialog width="400" center class="applyDialog" :model="formData" :open.sync="isShowApply">
            <p class="dialogTitle">报名信息</p>
            <div class="">
                <i class="iconfont icon-My"></i>
                <input class="" v-model="formData.memberName" type="text" placeholder="请输入姓名">
            </div>
            <div>
                <i class="iconfont icon-shouji"></i>
                <input type="text" v-validate="'required|memberMobile'" name="mobile" v-model="formData.memberMobile" placeholder="请输入手机号">
                <span v-show="errors.has('mobile')" class="error">{{ errors.first('mobile')}}</span>

            </div>
            <div>
                <i class="iconfont icon-neirong"></i>
                <input type="text" v-model="formData.remark" placeholder="备注">

            </div>
            <mu-button class="applyBtn" @click="closeApply()">确认</mu-button>
            <mu-button class="applyBtn" @click="cancelApply">取消</mu-button>
        </mu-dialog>
    </div>
</template>

<script>
    import Header from "@/components/Header.vue"
    import Footer from "@/components/Bottom.vue"
    import { Toast } from 'mint-ui'
    import { Popup } from 'vant';
    import * as Cookies from 'js-cookie'
    import VeeValidate, { Validator } from 'vee-validate'
    Validator.extend('memberMobile', {
        getMessage: name =>'必须是11位手机号码',
        validate: value => {
            return value.length == 11 && /^((13|14|15|17|18)[0-9]{1}\d{8})$/.test(value)
        }
    });
    export default {
        components: {
            Header,
            Footer,
            Toast
        },
        data() {
            return {
                isShowApply: false,
                activityDetail: [],
                commentList: [],
                // isShowApply:true,
                formData: {
                    // activityId: "",
                    remark: "",
                    memberName: "",
                    memberMobile: ""
                },
                good: 0,
                id: "",
                countComment: "",

                share: false,
                config: {
                    // url                 : '', // 网址，默认使用 window.location.href
                    // source              : '', // 来源（QQ空间会用到）, 默认读取head标签：<meta name="site" content="http://overtrue" />
                    // title               : '', // 标题，默认读取 document.title 或者 <meta name="title" content="share.js" />
                    // description         : '', // 描述, 默认读取head标签：<meta name="description" content="PHP弱类型的实现原理分析" />
                    // image               : '', // 图片, 默认取网页中第一个img标签

                    sites: ["qzone", "qq", "weibo", "wechat"], // 启用的站点
                    // disabled            : ['google', 'facebook', 'twitter','douban], // 禁用的站点
                    wechatQrcodeTitle: "微信扫一扫：分享", // 微信二维码提示文字
                    wechatQrcodeHelper:
                        "<p>微信里点“发现”，扫一下</p><p>二维码便可将本文分享至朋友圈。</p>"
                },
            }
        },
        methods: {
            // 打开报名框
            handleApply() {
                if (this.activityDetail.status != 1) {
                    this.isShowApply = false
                }
                this.isShowApply = true;
            },
            cancelApply() {
                this.isShowApply = false
            },
            // 确认报名 关闭报名框
            closeApply() {
                this.$validator.validateAll().then((result) => {
                    if (result) {
                        let activityId = this.$route.query.id
                        this.$axios.get(`/jsp/wap/trActivity/do/doSignUp.jsp`, {
                            params: {
                                activityId,
                                memberName: this.formData.memberName,
                                memberMobile: this.formData.memberMobile,
                                remark: this.formData.remark
                            }
                        }).then(res => {
                            console.log("活动报名", res)

                            if (res.success == "true") {
                                let instance = Toast('报名成功');
                                setTimeout(() => {
                                    instance.close();
                                }, 2000);
                                // }
                            } else {
                                let instance = Toast(res.message);
                                setTimeout(() => {
                                    instance.close();
                                }, 2000);
                            }
                        })
                        setTimeout(() => {
                            this.isShowApply = false;
                        }, 500);
                        return;
                    }
                    let instance = Toast('请输入正确的手机号');
                    setTimeout(() => {
                        instance.close();
                    }, 2000);
                });
            },
            // 活动详情
            getActivityDetail() {
                this.id = this.$route.query.id
                this.$axios.get(`/jsp/wap/trActivity/ctrl/jsonActivityDetail.jsp?id=${this.id}`).then(res => {
                    console.log("111", res)
                    this.activityDetail = res.data
                    this.activityDetail.greatNum = Number(res.data.greatNum)
                    if (Cookies.get('userKey') && this.$store.state.userinfo.headImgPath != '') {
                        this.avatar = this.$store.state.userinfo.headImgPath
                    }
                    if (Cookies.get('userKey') && this.$store.state.userinfo.name != '') {
                        this.memberName = this.$store.state.userinfo.name
                    }
                    if (Cookies.get('userKey') && this.$store.state.userinfo.provinceStr != '') {
                        this.provinceStr = this.$store.state.userinfo.provinceStr
                    }
                })
            },
            // 是否点赞
            getGood() {
                this.$axios.get(`/jsp/wap/trActivity/do/isGreat.jsp?id=${this.id}`).then(res => {
                    console.log("是否点赞", res)
                    this.good = Number(res.data)
                })
            },
            // 点赞
            noGood() {
                this.$axios.get(`/jsp/wap/trActivity/do/doGreat.jsp?id=${this.id}`).then(res => {
                    console.log("点赞成功", res)
                    if (res.success == "true") {
                        let instance = Toast('点赞成功');
                        setTimeout(() => {
                            instance.close();
                        }, 500);
                        this.good = 1
                        this.activityDetail.greatNum = Number(this.activityDetail.greatNum + 1)
                    }
                })
            },
            // 取消点赞
            isGood() {
                this.$axios.get(`/jsp/wap/trActivity/do/cancelGreat.jsp?id=${this.id}`).then(res => {
                    console.log("取消点赞", res)
                    if (res.success == "true") {
                        let instance = Toast('已取消点赞');
                        setTimeout(() => {
                            instance.close();
                        }, 500);
                        this.good = 0
                        this.activityDetail.greatNum = Number(this.activityDetail.greatNum - 1)
                    }
                })
            },
            // 评论列表
            getComment() {
                this.id = this.$route.query.id
                this.$axios.get(`/jsp/wap/trActivity/ctrl/jsonCommentPage.jsp?id=${this.id}`).then(res => {
                    this.countComment = Number(res.data.pagination.totalCount)
                })
            }
        },
        created() {
            this.getActivityDetail()
            this.getGood()
            this.getComment()

        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    .error{
        color: #f00;
        font-size: .2rem
    }
    .containerAll {
        background: #f3f5f7;
        margin-bottom: 1rem
    }

    .end {
        background: #ccc !important
    }

    img {
        width: 100% 
    }

    .detailImg {
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

    .apply {
        width: 1.7rem;
        height: 1.7rem;
        position: fixed;
        bottom: 1.8rem;
        right: .4rem;
        background: #005982;
        border-radius: 50%;
        color: #fff;
        text-align: center;

        .icon-bianji1::before {
            display: block;
            font-size: .5rem;
            margin-top: .15rem;
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
        /* width: 90%; */
        background: #005982;
        color: #fff;
        text-align: left;
        margin-top: .4rem;
    }

    .shareBox {
        padding: .5rem;
        text-align: center;
    }

    .cancelShare {
        margin-top: .3rem;
        border: 1px solid #005982;
        border-radius: .1rem;
        width: 50%;
        text-align: center;
        margin: .3rem auto 0
    }
</style>