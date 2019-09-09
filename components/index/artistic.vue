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
          <img :src="item.img" alt />
          <ul class="cbody">
            <li class="title">{{item.title}}</li>
            <li class="pos">{{item.pos}}</li>
            <li class="price">
              ￥
              <em>{{item.price}}</em>
              <span>/起</span>
            </li>
          </ul>
        </el-card>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data: function() {
    return {
      kind: "all",
      list: {
        all: [],
        part: [],
        spa: [],
        movie: [],
        travel: []
      }
    };
  },
  computed: {
    cur: function() {
      return this.list[this.kind];
    }
  },

  //over通过mouseover事件触发，解决刷新没有数据问题
  async mounted() {
      let self = this;
    let {
      status,
      data: { count, pois }
    } = await self.$axios.get("/search/resultsByKeywords", {
      params: {
        keyword:'景点',
        city: this.$store.state.geo.position.city
      }
    });
    if (status === 200 && count > 0) {
      let r = pois
        .filter(item => item.photos.length)
        .map((item, index) => {
          return {
            title: item.name,
            pos: item.type.split(";")[0],
            price: item.biz_ext.cost || "暂无",
            img: item.photos[0].url,
            url: "//abc.com"
          };
        });
      this.list[this.kind] = r.slice(0, 9);
    } else {
      this.list[this.kind] = [];
    }
  },
  methods: {
    over: async function(e) {
      let dom = e.target;
      let tag = dom.tagName.toLowerCase();
      let self = this;
      // console.log(tag)
      if (tag === "dd") {
        this.kind = dom.getAttribute("kind");
        let keyword = dom.getAttribute("keyword");
        let {
          status,
          data: { count, pois }
        } = await self.$axios.get("/search/resultsByKeywords", {
          params: {
            keyword,
            city: this.$store.state.geo.position.city
          }
        });
        if (status === 200 && count > 0) {
          let r = pois
            .filter(item => item.photos.length)
            .map((item, index) => {
              return {
                title: item.name,
                pos: item.type.split(";")[0],
                price: item.biz_ext.cost || "暂无",
                img: item.photos[0].url,
                url: "//abc.com"
              };
            });
          this.list[this.kind] = r.slice(0, 9);
        } else {
          this.list[this.kind] = [];
        }
      }
    }
  }
};
</script>

<style lang='scss'>
@import "@/assets/css/index/artistic.scss";
</style>