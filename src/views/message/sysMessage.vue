<template>
    <div class="">
        <div v-infinite-scroll="loadMore" infinite-scroll-disabled="loading">
            <div v-for="(item,index) in systemData" :key="index" class="messageBox">
                <div class="desc">
                    <span v-if="item.noticeType == 0">系统</span>
                    <span v-if="item&&item.addTimeStr">{{item.addTimeStr.slice(0,10)}}</span>
                </div>
                <div class="messageTitle">{{item.content}}</div>
            </div>
        </div>
        <div v-show="noShow" class="noChange">还没有系统消息哦</div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                systemData: [],
                noShow: false,
                loading: false,
                pn: 1,
                pageNumber: 1,
                totalCount: '',
            }
        },
        methods: {
            // 上拉加载
            loadMore() {
                this.pn = this.pn + 1
                this.loading = true
                this.$axios.get(`/jsp/wap/center/ctrl/jsonNoticeList.jsp`, { params: { pageNumber: this.pn } }).then(res => {
                    if (res.success == "true") {
                        this.systemData = [...this.systemData, ...res.data.pageList]
                        this.totalCount = Number(res.data.pagination.totalCount)
                        this.loading = false
                    }
                })
            },
            // 获取系统消息
            getData() {
                this.$axios.get(`/jsp/wap/center/ctrl/jsonNoticeList.jsp`).then(res => {
                    console.log("系统消息", res)
                    if (res.success == "true") {
                        this.systemData = res.data.pageList
                        this.totalCount = Number(res.data.pagination.totalCount)
                        this.pn = 1
                        this.loading = false
                    }
                    if (this.systemData.length == 0) {
                        this.noShow = true
                    }

                })
            },

            // 
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
            line-height:2;
            font-family: "PingFang";
            color: rgb( 51, 51, 51);
        }
    }

    .noChange {
        text-align: center;
        color: #ccc;
        margin-top: 2rem
    }
    .desc{
        color: #999
    }
</style>