<template>

    <div class="all">
        <Header></Header>
        <div class="containerAll">
            
            <div class="detail">
                <div class="clearfix investors">
                    <div><img class="fll" src="../../../static/app/img/usrname.jpg" style="width:1.2rem"></div>
                    <div>
                        <div class="name">李世宏（董事长）</div>
                        <div class="company">北京开拓明天科技有限公司</div>
                    </div>
                </div>
                <div class="message">
                    
                    <div>
                        <span>所属行业:</span>
                        <span>互联网</span>
                    </div>
                    <div>
                        <span>所在地区:</span>
                        <span>北京</span>
                    </div>
                    <div>
                        <span>关注行业:</span>
                        <span>人工智能、大数据、物联网</span>

                    </div>
                    <div>
                        <span>类&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp型:</span>
                        <span>企业资金</span>

                    </div>
                    <div>
                        <span>法定代表人:</span>
                        <span>张黎明</span>

                    </div>
                    <div>
                        <span>注册资本:</span>
                        <span>500万元人民币</span>

                    </div>
                    <div>
                        <span>成立日期: </span>
                        <span>2018年10月10日---2049年10月10日</span>

                    </div>
                    <div>
                        <span>住&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp所:</span>
                        <span>北京市海淀区中国农大创业园</span>

                    </div>
                    <div>
                        <span>经营范围:</span>
                        <span>人工智能</span>

                    </div>
                    <div>
                        <span>联&nbsp&nbsp系&nbsp&nbsp人:</span>
                        <span>张黎明</span>

                    </div>

                </div>
                <div class="contentTell">
                    <div class="detaila">
                        <div class="peojectTitle">企业介绍及财务数据</div>
                    </div>
                    <div class="contentDesc">GLG格理集团是一个以领先技术驱动的专业平台，连接全球范围内的顶尖专家和专业人士。全球超过1</div>
                </div>
                <div class="contentTell">
                    <div class="detaila">
                        <div class="peojectTitle">投资能力&风险承担能力介绍</div>
                    </div>
                    <div class="contentDesc">我们的专家团由超过50万专业人士组成，即使在世界各地有着繁忙的日程，他们也坚持每天回答客户最具</div>
                </div>
                <div class="contentTell ">
                    <div class="detaila" @click="tomoreProject">
                        <div class="peojectTitle">TA的更多项目<i class="iconfont icon-xiangyou flr"></i></div>
                    </div>
                    <!-- <div class="mayProject" v-for="(item,index) in projectList" :key="index">
                        <div class="mayTitle">
                            {{item.title}}
                        </div>
                        <div class="mayTime">
                            <span>投资金额：</span>
                            <span>{{item.investAmountName}}</span>
                        </div>
                        <div class="mayTime">
                            <span>{{item.capitalSourceName}}</span>
                        </div>
                    </div> -->
                </div>
            </div>
        </div>
        <!-- <Footer class="footer"></Footer> -->
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
                memberInfo:[],
                projectDetail:[],
                projectList:[],
                memberId:"",
                loading: false,
                id:""
            }
        },
        methods:{
            // 投资详情
            getMoneyDetail() {
                this.id = this.$route.query.id
                this.$axios.get(`/jsp/wap/trProject/ctrl/jsonProjectDetail.jsp?id=${this.id}`).then(res => {
                    console.log("投资详情", res)
                    this.projectDetail = res.data.project
                    this.memberInfo = res.data.memberInfo
                    this.memberId = res.data.memberInfo.id
                    this.projectList = res.data.projectList  
                })
            },
             tomoreProject(){
                let id = this.$route.query.id
                this.$router.push({name:'moreProject',query:{memberId:this.memberId}})
            }
        },
        created(){
            this.getMoneyDetail()
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
        margin-top: .9rem
    }
    .investors{
        border-top: 1px solid #f3f5f7;
        background: #fff;
        padding: .2rem 0;
    }
    .company{
        font-size: .3rem;
        color: rgb( 153, 153, 153 );
        line-height: 1.4;
    }
    .name{
        font-size: .32rem;
        color: rgb( 51, 51, 51 );
        font-weight: bold;
        line-height: 1.8;
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
        padding: .1rem .2rem;
        line-height: 1.25;
        font-family: "PingFang";
        font-size: .23rem;
        font-weight: bold;
        opacity: .7;
        margin-right: .3rem
    }

    .likeBtn {
        // color: #ccc;
        // border: 1px solid #ccc;
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
        padding: .15rem 0;
        border-bottom: .05rem solid #f3f5f7

    }

    .mayTitle {
        color: rgb( 51, 51, 51);
        line-height: 1.6
    }

    .mayTime {
        line-height: 2;
        color: rgb(128, 128, 128);
    }
    .message{
        background: #fff;
        padding: .2rem;
        margin-bottom: .3rem
    }
    .message div{
        line-height: 2
    }
    .message div span:nth-child(1){
        font-family: "PingFang";
        color: rgb(137, 137, 137);
        display: inline-block;
        margin-right: .1rem
    }
</style>