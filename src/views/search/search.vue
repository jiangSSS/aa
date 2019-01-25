<template>
    <div>
        <div class="header clearfix">
            <div class="search fll">
                <div class="fll select">
                    <div class="leftHeader">
                        <!-- <span class="fll radioItem">项目</span> -->
                        <!-- <div class="type" v-show="isShow">
                            <span class="radioItem" v-model="type" v-for="(item,index) in searchList" :key="index">{{item}}</span>
                        </div> -->
                        <select class="radioItem" v-model="type" placeholder="请选择">
                            <option value="1">找资金</option>
                            <option value="2">找项目</option>
                            <option value="3">找资讯</option>
                            <option value="4">找活动</option>
                        </select>
                    </div>
                    <!-- <div class="sbuTitle fll">
                        <i class="iconfont icon-xiangxia" v-if="!isShow" @click="handleShowList"></i>
                        <i class="iconfont icon-xiangshang" v-else @click="handleCloseList"></i>
                    </div> -->
                </div>
                <input type="text" placeholder="请输入内容" v-model="title" class="input_search" />
                <i class="iconfont icon-sousuo1" @click="search"></i>
            </div>
            <div class="fll cancel" @click="$router.push('/')">取消</div>
        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                isShow: false,
                searchList: ["项目", "资金", "资讯"],
                type: '1',
                title: ""
            }
        },
        methods: {
            handleShowList() { this.isShow = true },
            handleCloseList() { this.isShow = false },
            search() {
                console.log("111")
                if (this.type == '1') {
                    this.$router.push({ name: "searchMoney", query: { title: this.title } })
                } else if (this.type == '2') {
                    this.$router.push({ name: "searchProject", query: { title: this.title } })
                } else if (this.type == '3') {
                    this.$router.push({ name: "searchNews", query: { title: this.title } })
                } 
                else if (this.type == '4') {
                    this.$router.push({ name: "searchActivity", query: { title: this.title } })
                }
            },
        }
    }
</script>
<style scoped lang="scss">
    .header {}

    .select {
        width: 1.5rem;
    }

    .search {
        margin: .2rem;
        background: #f3f5f7;
    }

    .leftHeader {}

    .icon-sousuo1 {
        line-height: 2;
        margin-right: .2rem
    }

    .input_search {
        border: 0;
        color: rgb( 153, 153, 153);
        width: 4rem;
        border-radius: 4px;
        font-family: "PingFang";
        line-height: 2.103;
        padding: 0 .2rem;
        background: #f3f5f7
    }

    .input_search:focus {
        outline: none;
    }

    .input_search::-webkit-input-placeholder {
        padding-left: .3rem
    }

    .cancel {
        line-height: 3.5;
        margin: 0 .2rem
    }

    .type {
        /* background: #f3f5f7 */
    }

    .radioItem {
        display: block;
        margin: 0 .1rem;
        border: 0;
        background: #f3f5f7;
        margin-top: .1rem
    }

    .radioItem:focus {
        border: 0
    }

    .sbuTitle {
        /* background: #f3f5f7 */
    }
</style>