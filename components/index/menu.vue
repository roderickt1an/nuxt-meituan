<template>
  <div class="m-menu">
    <dl class="nav" @mouseleave="mouseleave">
      <dt>全部分类</dt>
      <dd v-for="(item, index) in menu" :key="index" @mouseenter="enter">
        <i :class="item.type"></i>{{item.title}}<span class="arrow"></span>
      </dd>
    </dl>
    <div class="detail" v-if="kind" @mouseenter="sover" @mouseleave="sout">
      <template v-for="(item, index) in curdetail.child" >
        <h4 :key="index">{{item.name}}</h4>
        <span v-for="v in item.child" :key="v">{{v}}</span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      kind: '',
      menu: [{
        type: "food",
        title: "美食",
        child: [{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      },{
        type: "takeout",
        title: "外卖",
        child: [{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      },{
        type: "hotel",
        title: "外卖",
        child: [{
          name: "外卖",
          child: ['美团外卖']
        },{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      },{
        type: "food",
        title: "美食",
        child: [{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      },{
        type: "takeout",
        title: "外卖",
        child: [{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      },
      {
        type: "hotel",
        title: "外卖",
        child: [{
          name: "美食",
          child: ['代金券','甜点饮品','火锅']
        }]
      }]
    }
  },
  computed: {
    curdetail: function(){
      return this.menu.filter((item) => item.type === this.kind)[0]
    }
  },
  methods: {
    mouseleave(){
      let self = this
      self._timer = setTimeout(()=>{
        self.kind = ''
      }, 150)
    },
    enter(e){
      this.kind = e.target.querySelector("i").className
    },
    sover(){
      clearTimeout(this._timer)
    },
    sout(){
      this.kind = ''
    }
  }
}
</script>
