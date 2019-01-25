<template>
    

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
                isActive: 0,
                isActive1: 0,
                isActive2: [],
                checked: [],
                result: [],
                typeList: ["全部", "债权融资", "股权融资", "整体转让", "其他融资"],
                moneyType: ["个人资金", "企业资金", "天使投资", "VC投资", "PE投资", "小额贷款", "典当公司"],
                checkBox: [
                    {
                        title: "融资方式",
                    },
                    {
                        title: "融资方式",
                    },
                ]
            };
        },
        methods: {
            // 下拉/收起
            handleShowList() {this.isShow = true },
            handleCloseList() {this.isShow = false},
            handleShowList1() {this.isShow1 = true },
            handleCloseList1() {this.isShow1 = false},
            handleShowList2() { this.isShow2 = true},
            handleCloseList2() {this.isShow2 = false },
            handleShowList3() {this.isShow3 = true},
            handleCloseList3() {this.isShow3 = false},
            
            
        },
        
    };
</script>
<style scoped lang="scss">
    .chooseBox {
        background: #fff; 
        z-index: 1000;
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
        width: 1.6rem;
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
    .checkItem{
        width: 100%;
        padding: 0 .2rem;
        line-height: 2;
        border-bottom: 1px dashed #f3f5f7;
    }
</style>