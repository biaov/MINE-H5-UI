# Grid 宫格

----

## 按需引入

:::demo

```JavaScript
import Vue from "vue";
import { MeGrid, MeGridItem } from "mine-h5-ui";

Vue.use(MeGrid);
Vue.use(MeGridItem);
```

:::

## 复制

* 如果你觉得重新编写 HTML 结构麻烦，可以直接复制下面的代码。

## 代码演示

### 基础用法

* 通过在 `MeGrid` 组件上的 `cols` 属性来设置一行需要展示几个格子，默认为 4。
* 通过在 `MeGridItem` 组件上的 `icon` 和 `text` 属性来设置里面的图标和内容。

```HTML
<me-grid :cols="4">
  <me-grid-item icon="icon-wechat" text="微信"></me-grid-item>
</me-grid>
```

### 自定义用法

* 通过 `Slot` 来设置自定义内容。

```HTML
<template>
  <!-- 演示demo -->
  <div class="m-demo">
    <me-grid border-color="#d9d9d9" :cols="3" @on-change="onChange">
      <me-grid-item v-for="item in grids" :keys="item.icon" v-bind="item" @on-click="handleLi(item)"></me-grid-item>
      <me-grid-item>
        <div class="u-cust">
          <me-icon name="icon-love" color="#999" size="28px"></me-icon>
          <p>自定义内容</p>
        </div>
      </me-grid-item>
    </me-grid>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // 格子列表
      grids: [
        {
          icon: "icon-wechat",
          text: "微信",
          iconColor: "#67c23a"
        },
        {
          icon: "icon-pengyouquan",
          text: "朋友圈",
          iconColor: "#409eff"
        },
        {
          icon: "icon-zhifubao",
          text: "支付宝",
          iconColor: "#06b4fd"
        },
        {
          icon: "icon-qq",
          text: "QQ",
          iconColor: "#ec502b"
        },
        {
          icon: "icon-weibo",
          text: "微博",
          iconColor: "#f40f3b"
        },
        {
          icon: "icon-qr-code",
          text: "二维码",
          iconColor: "#1cc09e"
        },
        {
          icon: "icon-xiangji",
          text: "相机",
          iconColor: "#4a82ff"
        },
        {
          icon: "icon-loading_ico",
          text: "加载",
          iconColor: "#f60",
          textColor: "#ff9249"
        }
      ]
    };
  },
  methods: {
    // 点击格子项
    handleLi({ text }) {
      this.$MeToast(text);
    },
    // 点击第几个
    onChange(index) {
      console.log(`你点击了第${index + 1}个`);
    }
  }
};
</script>
<style scoped lang="less">
.m-demo {
  // 自定义内容
  .u-cust {
    .me-icon {
      position: relative;
      display: block;
      margin: 0 auto 5px;
      &::after {
        content: "";
        position: absolute;
        top: -4px;
        right: 20px;
        border-radius: 50%;
        width: 14px;
        height: 14px;
        background: #f66;
      }
    }
  }
}
</style>
```

## API

### MeGrid

#### 参数

| 参数         | 说明         | 类型   | 可选值 | 默认值  |
|--------------|--------------|--------|--------|---------|
| cols         | 一行几个宫格 | Number | --     | 4       |
| border-color | 宫格边框颜色 | String | --     | #edeff2 |

#### Slots

* ⚠ 注意：此插槽只接 `MeGridItem` 组件。

| 具名插槽 | 说明     | scopedSlots |
|----------|----------|-------------|
| default  | 默认名称 | --          |

#### 方法

| 方法名    | 说明                     | 回调参数     |
|-----------|--------------------------|--------------|
| on-change | 点击单个宫格时触发的事件 | index:索引值 |

### MeGridItem

#### 参数

| 参数       | 说明                 | 类型   | 可选值 | 默认值  |
|------------|----------------------|--------|--------|---------|
| icon       | 单个宫格项的图标     | String | --     | --      |
| icon-color | 单个宫格项图标的颜色 | String | --     | #494949 |
| text       | 单个宫格项的文本     | String | --     | --      |
| text-color | 单个宫格项文本的颜色 | String | --     | #949494 |

#### 方法

| 方法名   | 说明                     | 回调参数    |
|----------|--------------------------|-------------|
| on-click | 点击单个宫格时触发的事件 | Event:event |
