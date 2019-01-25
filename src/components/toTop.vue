<template>
    <div class="">
        <a class="totop" id="totop" @click="goTop">
            <img src="../../static/app/img/backTop.png" alt="">
        </a>
    </div>
</template>

<script>
    export default {
        data() {

            return {
                // toTopShow: true,
                // isTop: true,
                // timer: null
            };
        },
        mounted() {
            // this.goTop()
            // window.addEventListener('onscroll', function () {

            // })
            // var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
            // console.log(scrollTop);

        },
        
        methods: {
            goTop() {
                var scrollTop = 0;
                if (document.documentElement && document.documentElement.scrollTop) {
                    scrollTop = document.documentElement.scrollTop;
                }
                else if (document.body) {
                    scrollTop = document.body.scrollTop;
                }
                console.log(scrollTop)
                console.log(document.body.scrollTop)
                console.log(document.documentElement.scrollTop)         
            },
            nexttick(){
                var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
                console.log(scrollTop);
            }
            

        },
    };
</script>
<style scoped lang="scss">
    .totop {
        position: fixed;
        right: 0.8rem;
        bottom: 1.5rem;
        cursor: pointer;
    }
</style>