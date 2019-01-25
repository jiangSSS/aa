<template>
    <div class="">
        <div v-for="(item,index) in projectData" :key="index" class="messageBox">
            <div class="messageTitle">{{item.title}}</div>
            <div class="messageDetail">{{item.content}}</div>
            <img :src=" $url + imgPaths" alt="" v-for="(imgPaths,idx) in item.imgPathList" :key="idx" class="imgList">
            <div class="time">
                <i class="iconfont icon-shijian"></i>
                <span class="seconed">{{item.addTimeStr.slice(0,10)}}</span>
                <span class="seconed">{{item.addTimeStr.slice(10,19)}}</span>
            </div>
            <!-- <div class="messageTime">{{item.time}}</div> -->
        </div>
        <div v-show="noShow" class="noChange">您关注的项目还未发布进展</div>
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
                projectData: [],
                noShow: false
            }
        },
        methods: {
            getData() {
                this.$axios.get(`/jsp/wap/center/ctrl/jsonDynamicList.jsp?type=1`).then(res => {
                    console.log("项目进展", res)
                    this.projectData = res.data
                    if (this.projectData.length == 0) {
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
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            border-left: 3px solid #005982;
            padding-left: .2rem;
            margin: .2rem 0;
            
        }
        .messageDetail {
            font-size: .28rem;
            font-family: "PingFang";
            line-height: 2;
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

    .imgList {
        width: 2.25rem;
        padding-right: .2rem;
        height: 1.5rem;
    }

    .seconed {
        color: #999
    }
</style>