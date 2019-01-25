<template>
    <div>
        <Header></Header> 
            <div class="detail">
                    <img src="/static/img/search.jpg" alt="">
                    <img src="/static/img/invest2.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
                <img src="/static/img/content-invest.jpg" alt="">
            </div>
        <Footer class="footer"></Footer>
    </div>
</template>

<script>
    import Header from "@/components/Header.vue"
    import Footer from "@/components/Bottom.vue"
    export default {
        components: {
            Footer,
            Header
        },
        data() {
            return {
            }   
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .detail {
        padding-bottom: .8rem;
        padding-top: .8rem
    }

    .all {
        position: relative;
        width: 100%
    }

    img {
        width: 100%
    }

    .header {
        width: 100%;
        position: fixed;
        top: 0;
        right: 0;
    }

    .footer {
        width: 100%;
        position: fixed;
        bottom: 0;
        right: 0;
    }

    .tab {
        /* width: 20%; */
        display: flex;
        justify-content: space-between;
        padding: .3rem 0
    }

    .tab img {
        width: 90%;
        height: 2rem
    }
</style>