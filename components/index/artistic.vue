<template>
    <section class="m-istyle">
        <dl @mouseover="over">
            <dt>有格调</dt>
            <dd :class="{active:kind === 'all'}" kind="all" keyword="景点">全部</dd>
            <dd :class="{active:kind === 'part'}" kind="part" keyword="美食">聚餐</dd>
            <dd :class="{active:kind === 'spa'}" kind="spa" keyword="丽人">丽人SPA</dd>
            <dd :class="{active:kind === 'movie'}" kind="movie" keyword="电影">电影出演</dd>
            <dd :class="{active:kind === 'travel'}" kind="travel" keyword="旅游">品质出游</dd>
        </dl>
        <ul class="ibody">
            <li v-for="item in cur" :key="item.title">
                <el-card :body-style="{padding:'0px'}" shadow="never">
                    <img :src="item.img" alt="">
                    <ul class="cbody">
                        <li class="title">{{item.title}}</li>
                        <li class="pos">{{item.pos}}</li>
                        <li class="price">￥<em>{{item.price}}</em><span>/起</span></li>
                    </ul>
                </el-card>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    data:function(){
        return {
            kind:'all',
            list:{
                all:[{
                    title:'必胜客',
                    pos:'【限时半价】',
                    price:'63.5',
                    img:'//p1.meituan.net/msmerchant/bfe262afe900dc84e2de9902d1eb8e222117414.jpg@460w_260h_1e_1c'
                }],
                part:[],
                spa:[],
                movie:[],
                travel:[]
            }
        }
    },
    computed:{
        cur:function(){
            return this.list[this.kind]
        }
    },
    methods:{
        over:function(e){
            let dom = e.target
            let tag = dom.tagName.toLowerCase()
            // console.log(tag)
            if(tag === 'dd'){
                this.kind = dom.getAttribute('kind')
                let keyword = dom.getAttribute('keyword')
                if(this.kind === 'part'){
                    this.list[this.kind] = [{
                        title:'八合里海记',
                        pos:'提供免费wifi',
                        price:'128',
                        img:'//p1.meituan.net/msmerchant/d504871aed2dd62da8172fe2c093df03121351.jpg@460w_260h_1e_1c'
                    }]
                }if (this.kind === 'spa') {
                    this.list[this.kind] = [{
                        title:'横店电影城',
                        pos:'免押金，可停车，儿童票',
                        price:'25',
                        img:'//p0.meituan.net/deal/__43558314__1826377.jpg@460w_260h_1e_1c'
                    }]
                }if (this.kind === 'movie') {
                    this.list[this.kind] = [{
                        title:'华夏太古巨幕影城',
                        pos:'可停车，巨幕厅',
                        price:'23',
                        img:'//p1.meituan.net/mogu/b1009f362b0fe2f69e8a85588fb6d0b7214982.jpg@460w_260h_1e_1c'
                    }]
                }if(this.kind === 'travel'){
                    this.list[this.kind] = [{
                        title:'湖南华天大酒店',
                        pos:'预约发票，酒店套餐',
                        price:'426',
                        img:'//p0.meituan.net/tdchotel/c2b5edc79a0108b4534750ae5576a05070707.jpg@460w_260h_1e_1c'
                    }]
                }
            }
        }
    }
}
</script>

<style lang='scss'>
    @import "@/assets/css/index/artistic.scss"
</style>