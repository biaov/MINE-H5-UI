<template>
  <!-- 标签选项 -->
  <div class="me-tab-item" v-show="isShow">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: "MeTabItem",
  props: {
    // 标签内容
    title: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      currentId: 0, // 当前 id
      isShow: false // 是否显示
    };
  },
  methods: {
    // 设置下标数据
    setData(id) {
      this.currentId = id;
      this.initShow();
    },
    // 点击列表项
    handleClick() {
      const {
        $parent: { $options, onChange },
        currentId
      } = this;
      $options._componentTag === "me-tab" && onChange(currentId); // 向父组件传递数据
      this.$emit("on-click");
    },
    // 设置初始化显示
    initShow() {
      const {
        $parent: { $options, value },
        currentId
      } = this;
      this.isShow = $options._componentTag === "me-tab" && currentId === value;
    }
  }
};
</script>