<template>
  <div class="m-menu">
    <dl class="nav" @mouseleave="mouseLeave">
      <dt>全部分类</dt>
      <dd v-for="(item, i) in menu" :key="i" @mouseenter="mouseEnter($event, item.type)">
        <i :class="item.type" />{{ item.title }}<span class="arrow" />
      </dd>
    </dl>
    <div
      v-if="kind"
      class="detail"
      @mouseenter="sover"
      @mouseleave="sout"
    >
      <template v-for="(item, index) in curDetail.child">
        <h4 :key="index">{{ item.title }}</h4>
        <span v-for="c in item.child" :key="c">{{ c }}</span>
      </template>
    </div>
  </div>
</template>

<script>
  export default {
    name: "menu",
    data() {
      return {
        kind: '',
        menu: [
          {
            type: 'food',
            title: '美食',
            child: [
              {
                title: '美食',
                child: ['代金券', '甜点饮品', '火锅', '自助餐', '小吃快餐']
              }
            ]
          },
          {
            type: 'takeout',
            title: '外卖',
            child: [
              {
                title: '外卖',
                child: ['美团外卖']
              }
            ]
          },
          {
            type: 'hotel',
            title: '酒店',
            child: [
              {
                title: '酒店星级',
                child: ['经济型', '舒适/三星', '高档/四星']
              }
            ]
          },
        ],
      }
    },
    computed: {
      curDetail() {
        // filter返回数组
        return this.menu.filter(item => item.type === this.kind)[0]
      }
    },
    methods: {
      mouseLeave() {
        this._timer = setTimeout(() => {
          this.kind = ''
        }, 150)
      },
      mouseEnter(e, type) {
        this.kind = type
      },
      sover() {
        clearTimeout(this._timer)
      },
      sout() {
        this.kind = ''
      }
    },
    beforeDestroy() {
      clearTimeout(this._timer)
    }
  }
</script>

<style scoped>

</style>
