# CountDown 倒计时

----

## 按需引入

:::demo

```JavaScript
import Vue from "vue";
import { MeCountDown } from "mine-h5-ui";

Vue.use(MeCountDown);
```

:::

## 复制

* 如果你觉得重新编写 HTML 结构麻烦，可以直接复制下面的代码。

## 代码演示

### 基础用法

* 通过属性 `time` 来设置组件的倒计时间，单位为毫秒 (ms)。

```HTML
<me-count-down :time="2*60*60*1000"></me-count-down>
```

### 毫秒级渲染

* 通过属性 `format` 来设置组件的格式，完整格式为 `DD:hh:mm:ss:ms`,默认格式为 `hh:mm:ss`。

```HTML
<me-count-down :time="2*60*60*1000" format="hh:mm:ss:ms"></me-count-down>
```

## API

### 参数

| 参数      | 说明                                | 类型    | 可选值       | 默认值   |
|-----------|-------------------------------------|---------|--------------|----------|
| time      | 倒计时的时间，单位毫秒(ms)          | Number  | --           | --       |
| format    | 显示格式，完整格式 `DD:hh:mm:ss:ms` | String  | --           | hh:mm:ss |
| isStart   | 是否开始                            | Boolean | true / false | false    |
| isSuspend | 是否暂停                            | Boolean | true / false | false    |
| isReset   | 是否重置                            | Boolean | true / false | false    |

#### Slots

| 具名插槽 | 说明     | scopedSlots                |
|----------|----------|----------------------------|
| default  | 默认名称 | { hh: "", ms: "", ss: "" } |

### 方法

| 方法名      | 说明                   | 回调参数               |
|-------------|------------------------|------------------------|
| on-end      | 倒计时结束时触发的事件 | --                     |
| on-progress | 倒计时进行时触发的事件 | time: number(当前时间) |
