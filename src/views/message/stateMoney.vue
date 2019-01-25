<template>
    <div class="">
        <div v-for="(item,index) in MoneyData" :key="index" class="messageBox">
            <div>
                <div class="messageTitle">{{item.content}}</div>
                <div class="messageDetail">{{item.detail}}</div>
                <div class="messageTime">{{item.time}}</div>
            </div>
        </div>
        <div v-show="noShow" class="noChange">您关注的资金还未发布动态</div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                messageList: [
                    {
                        title: "北京某互联网创新创业服务平台项目",
                        detail: "感谢大家关注本项目，现已将正式投入研发，预计年底之前上线",
                        time: "2018-01-01  12:11:10"
                    },
                    {
                        title: "北京某互联网创新创业服务平台项目",
                        detail: "感谢大家关注本项目，现已将正式投入研发，预计年底之前上线",
                        time: "2018-01-01  12:11:10"
                    },
                    {
                        title: "北京某互联网创新创业服务平台项目",
                        detail: "感谢大家关注本项目，现已将正式投入研发，预计年底之前上线",
                        time: "2018-01-01  12:11:10"
                    },
                ],
                MoneyData: [],
                noShow: false
            }
        },
        methods: {
            getData() {
                this.$axios.get(`/jsp/wap/center/ctrl/jsonDynamicList.jsp?type=2`).then(res => {
                    console.log("资金动态", res)
                    this.MoneyData = res.data
                    if (this.MoneyData.length == 0) {
                        this.noShow = true
                    }
                })
            }
        },
        created() {
            this.getData()
        }

    }
</script>
<style scoped lang="scss">
    .detail {
        padding-top: .8rem;
        padding-bottom: .9rem;
    }

    img {
        width: 100%
    }

    .subTabs {
        // background: #fff
        padding: 0;
    }

    .subTab {
        font-size: .5rem !important;
        font-family: "PingFang";
        color: rgb( 51, 51, 51);
        line-height: 2.727;
        text-align: center;
        background: #fff
    }

    .messageBox {
        background: #fff;
        padding: .2rem;
        border-bottom: .2rem solid #f3f5f7;
        .messageTitle {
            font-size: .32rem;
            font-family: "PingFang";
            color: rgb( 51, 51, 51);
        }
        .messageDetail,
            {
            font-size: .28rem;
            font-family: "PingFang";
            color: rgb( 102, 102, 102);
        }
        .messageTime {
            color: #999;
            font-size: .26rem;
        }
    }

    .noChange {
        text-align: center;
        color: #ccc;
        margin-top: 2rem
    }
</style>