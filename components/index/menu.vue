<template>
    <div class="m-menu">
        <dl class="nav" @mouseleave="mouseleave">
            <dt>全部分类</dt>
            <dd v-for="(item,dex) in $store.state.home.menu" :key="dex" @mouseenter="enter">
                <i :class="item.type"/>{{item.name}}<span class="arrow"></span>
            </dd>
        </dl>
        <div class="detail" v-if="kind" @mouseenter="sover" @mouseleave="sout">
            <template v-for="(item,idx) in curdetail.child">
                <h4 :key="idx">{{item.title}}</h4>
                <span v-for="v in item.child" :key="v">{{v}}</span>
            </template>
      
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            kind:'',
            menu:[{
                type:'food',
                name:"美食",
                child:[{
                    title:'美食',
                    child:['火锅','烧烤','奶茶','水果','奶茶','水果','奶茶','水果','奶茶','水果','奶茶','水果','奶茶','水果']
                }]
            },{
                type:'takeout',
                name:"外卖",
                child:[{
                    title:'外卖',
                    child:['美团外卖']
                }]
            },{
                type:'hotel',
                name:"酒店",
                child:[{
                    title:'酒店星级',
                    child:['经济','舒适','豪华五星']
                }]
            }]
        }
    },
    computed:{
        curdetail:function(){
            return this.$store.state.home.menu.filter((item) =>item.type === this.kind)[0]
        }
    },
    methods:{
        mouseleave:function(){
            let self = this;
            self._timer=setTimeout(function(){
                self.kind = ''
            },150)
        },
        enter:function(e){
            this.kind=e.target.querySelector('i').className
        },
        sover:function(){
            clearTimeout(this._timer)
        },
        sout:function(){
            this.kind=''
        }
    }
}
</script>

<style lang='scss'>

</style> 