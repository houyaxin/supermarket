<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive">
      <slot name="item-icon"></slot>
    </div>
    <div v-else>
      <slot name="item-icon-active"></slot>
    </div>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props:{
    path: String,
    activeColor:{
      type: String,
      default: 'red'
    }
  },
  data() {
    return {
    };
  },
  computed:{
    isActive(){
      // this.$router 实际上就是全局路由对象任何页面都可以调用 push(), go()等方法
      //  this.$route 表示当前正在用于跳转的路由器对象，可以调用其name、path、query、params等属性
      return  this.$route.path.indexOf(this.path) !==-1
    },
    activeStyle(){
      return this.isActive ? {color: this.activeColor}:{}
    }
  },
  methods: {
    itemClick() {
      this.$router.replace(this.path)
    },
  },
};
</script>
<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}
.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle;
  margin-bottom: 2px;
}
.active {
  color: red;
}
</style>
