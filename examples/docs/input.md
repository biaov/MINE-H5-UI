# Input 输入框

----

## 按需引入

:::demo

```JavaScript
import Vue from "vue";
import { MeInput } from "mine-h5-ui";

Vue.use(MeInput);
```

:::

## 复制

* 如果你觉得重新编写 HTML 结构麻烦，可以直接复制下面的代码。

## 代码演示

### 基础用法

* 通过属性 `type` 设置输入框的类型，支持原生 type 类型，默认为 text。

```HTML
<me-input type="text" v-model="inputValue"></me-input>
```

### 自定义类型

* 通过属性 `label` 设置输入框的标签内容。

```HTML
<me-input v-model="inputValue" label="用户名" label-width="78px" placeholder="请输入用户名"></me-input>
<me-input v-model="inputValue" label="整数" label-width="78px" placeholder="请输入整数" :digit="true"></me-input>
<me-input v-model="inputValue" label="颜色自定" label-width="78px" label-color="#f60" placeholder="请输入文本"></me-input>
<me-input v-model="inputValue" label="图标" label-width="78px" label-color="#ec632f" label-icon="icon-star" placeholder="请输入文本"></me-input>
```

### 聚焦颜色

* 通过属性 `focus-type` 设置输入框的聚焦颜色，默认为 default 。

```HTML
<me-input v-model="inputValue" label="信息聚焦" focus-type="primary"></me-input>
<me-input v-model="inputValue" label="成功聚焦" focus-type="success"></me-input>
<me-input v-model="inputValue" label="警告聚焦" focus-type="warning"></me-input>
<me-input v-model="inputValue" label="危险聚焦" focus-type="danger"></me-input>
<me-input v-model="inputValue" label="自定聚焦" focus-color="#f100ff"></me-input>
```

### 图标按钮

* 通过属性 `icon` 设置输入框的图标。

```HTML
<me-input v-model="inputValue" label="密码" :password="true"></me-input>
<me-input v-model="inputValue" label="清理" icon="icon-close" @on-click-icon="handleIcon"></me-input>
```

### 短信验证码

* 通过属性 `sms-msg` 和 `sms-is` 设置输入框的短信验证码按钮的显示。

```HTML
<me-input v-model="inputValue" sms-msg="短信验证码" :sms-is="false"></me-input>
<me-input v-model="inputValue" sms-msg="短信验证码" sms-is="icon-close" sms-color="#549ff2" placeholder="自定义验证码颜色" @on-click-sms="handleSMS"></me-input>
```

### 禁用状态

* 通过属性 `readonly` 和 `disabled` 设置输入框的只读和禁用状态。

```HTML
<me-input v-model="inputValue" label="只读状态" :readonly="true"></me-input>
<me-input v-model="inputValue" label="禁用状态" :disabled="true"></me-input>
```

## API

### 参数

| 参数        | 说明               | 类型             | 可选值                                                                   | 默认值    |
|-------------|--------------------|------------------|--------------------------------------------------------------------------|-----------|
| v-model     | 双向绑定弹出层状态 | [String, Number] | --                                                                       | --        |
| type        | 输入框类型         | String           | 原生input类型                                                            | text      |
| placeholder | 输入框占位符       | String           | --                                                                       | 请输入... |
| label       | 输入框标签         | String           | --                                                                       | --        |
| label-width | 标签宽度           | String           | --                                                                       | --        |
| label-align | 标签对齐方式       | String           | auto / left / right / center / justify / start / end / initial / inherit | left      |
| label-color | 标签颜色           | String           | --                                                                       | --        |
| label-icon  | 标签图标           | String           | --                                                                       | --        |
| focus-type  | 聚焦类型           | String           | default / primary / success / warning / danger                           | default   |
| focus-color | 聚焦自定义颜色     | String           | --                                                                       | --        |
| icon        | 图标按钮           | String           | --                                                                       | --        |
| password    | 密码输入框         | Boolean          | true / false                                                             | false     |
| digit       | 整数输入框         | Boolean          | true / false                                                             | false     |
| sms-msg     | 短信验证码信息     | String           | --                                                                       | --        |
| sms-color   | 短信验证码颜色     | String           | --                                                                       | --        |
| sms-is      | 是否开启倒计时     | Boolean          | true / false                                                             | false     |
| readonly    | 只读               | Boolean          | true / false                                                             | false     |
| disabled    | 禁用               | Boolean          | true / false                                                             | false     |

### 方法

| 方法名        | 说明                           | 回调参数    |
|---------------|--------------------------------|-------------|
| on-click-icon | 点击图标时触发的事件           | --          |
| on-click-sms  | 点击短信验证码时触发的事件     | --          |
| on-focus      | 输入框聚焦时触发的事件         | event:Event |
| on-input      | 输入框输入时触发的事件         | event:Event |
| on-change     | 输入框内容发生改变时触发的事件 | event:Event |
| on-blur       | 输入框移除焦点时触发的事件     | event:Event |
