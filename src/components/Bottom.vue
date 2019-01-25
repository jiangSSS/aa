<template>

    <div class="tabs">
        <router-link to="/home" class="tab-item" :class="{active:$route.name === 'home'}">
            <i class="iconfont icon-shouye"></i>
            <div class="tab-title">首页</div>
        </router-link>
        <router-link to="/projectA" class="tab-item" :class="{active:$route.name === 'projectA'}">
            <i class="iconfont icon-icon-project"></i>
            <div class="tab-title">项目库</div>
        </router-link>
        <router-link to="/message" class="tab-item" :class="{active:$route.name === 'sysMessage'}">
            <i class="iconfont icon-xiaoxi"></i>
            <div class="tab-title">消息</div>
        </router-link>
        <router-link to="/money" class="tab-item" :class="{active:$route.name === 'money'}">
            <i class="iconfont icon-diamond"></i>
            <div class="tab-title">资金</div>
        </router-link>
        <div @click="person" class="tab-item" :class="{active:$route.name === 'my'}">
            <i class="iconfont icon-My"></i>
            <div class="tab-title">我的</div>
        </div>
    </div>
</template>

<script>
    import Header from "@/components/Header.vue"
    import * as Cookies from 'js-cookie'

    export default {
        components: {
            Header
        },
        data() {
            return {
                
            }
        },
        methods: {
            person() {
                if (Cookies.get('userKey')) {
                    this.$router.push('/my')
                } else {
                    this.$router.push('/login')
                }
            },
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
    .tabs {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        background-size: 100%; // height: 1.3rem;
        display: flex;
        background: #fff;
        padding: .1rem 0;
        a {
            text-decoration: none;
            color: #666
        }
        .tab-item {
            width: 2.5rem;
            flex: 1;
            text-align: center;
            .iconfont {
                font-size: .4rem;
            }
            ;
            .tab-title {
                font-size: .26rem;
                margin-top: -.1rem
            }
        }
        .active {
            color: #005982
        }
    }
</style>