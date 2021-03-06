<template>
  <!-- 输入框 -->
  <div class="me-input" :class="`me-input-${focusType}`">
    <div class="u-label" :style="`width:${labelWidth};text-align-last:${labelAlign};color:${labelColor};`" ref="label" v-if="!!label">
      <me-icon :name="labelIcon" :color="labelColor" size="inherit" v-if="!!labelIcon"></me-icon>{{label}}
    </div>
    <input :type="inputType" v-model="inputVal" class="u-input" :placeholder="placeholder" :style="`${isFocus&&`border-color:${focusColor};`};padding-right:${paddingRight}px;padding-left:${paddingLeft}px;`" @focus="onFocusBlur('on-focus',$event)" @blur="onFocusBlur('on-blur',$event)" @change="onEvent('on-change',$event)" @input="onEvent('on-input',$event)" :readonly="readonly" :disabled="disabled">
    <me-icon :name="inputType=='password'?'icon-in_biyan':'icon-in_zhengyan'" @on-click="handleIcon" v-if="password"></me-icon>
    <me-icon :name="icon" @on-click="handleIcon" v-else></me-icon>
    <span class="u-sms" :class="{countdown:smsIs}" v-if="!password&&!!smsMsg" @click="handleSMS" ref="sms" :style="`color:${smsColor};`">{{smsMsg}}</span>
  </div>
</template>
<script>
import MeIcon from "~/MeIcon";
export default {
  name: "MeInput",
  components: {
    MeIcon
  },
  props: {
    // input绑定值
    value: {
      type: [String, Number],
      default: ""
    },
    // 输入框值
    type: {
      type: String,
      default: "text"
    },
    // 占位符
    placeholder: {
      type: String,
      default: "请输入..."
    },
    // 只读状态
    readonly: {
      type: Boolean,
      default: false
    },
    // 禁用状态
    disabled: {
      type: Boolean,
      default: false
    },
    // label内容
    label: {
      type: String,
      default: ""
    },
    // label宽度
    labelWidth: {
      type: String,
      default: ""
    },
    // label对齐方式
    labelAlign: {
      type: String,
      default: "left" // auto|left|right|center|justify|start|end|initial|inherit;
    },
    // label颜色
    labelColor: {
      type: String,
      default: ""
    },
    // label图标
    labelIcon: {
      type: String,
      default: ""
    },
    // 聚焦边框样式
    focusType: {
      type: String,
      default: "default" // default|primary|success|warning|danger
    },
    // 聚焦颜色
    focusColor: {
      type: String,
      default: ""
    },
    // 图标
    icon: {
      type: String,
      default: ""
    },
    // 密码输入框
    password: {
      type: Boolean,
      default: false
    },
    // 整数输入
    digit: {
      type: Boolean,
      default: false
    },
    // 短信验证码
    smsMsg: {
      type: String,
      default: ""
    },
    // 短信颜色
    smsColor: {
      type: String,
      default: ""
    },
    // 是否开启倒计时
    smsIs: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      inputVal: this.value, // 输入框值
      inputType: "password", // 输入框type值
      paddingLeft: 0, // label宽度
      paddingRight: 0, // span宽度
      isFocus: false // 是否聚焦
    };
  },
  methods: {
    // 点击图标按钮
    handleIcon() {
      const { password, inputType } = this;
      // 判断是否是密码输入框
      if (password) {
        this.inputType = inputType === "password" ? "text" : "password";
      } else {
        this.$emit("on-click-icon");
      }
    },
    // 点击短信验证码
    handleSMS() {
      // 判断是否处于倒计时状态
      if (!this.smsIs) {
        this.$emit("on-click-sms");
      }
    },
    // 设置input的右侧padding
    setInputPadding(type) {
      const { labelWidth, label, $refs, smsMsg } = this;
      // 0:左侧,1:右侧
      if (type === 1) {
        this.paddingRight = !smsMsg ? 10 : $refs.sms.offsetWidth; // 设置input右侧padding
      } else {
        // 设置input左侧padding
        this.paddingLeft = !label ? 10 : Math.max(parseFloat(labelWidth || 0), $refs.label.offsetWidth);
      }
    },
    // 输入框聚焦和失去焦点
    onFocusBlur(name, e) {
      // type:focus->聚焦,blur->失去焦点
      this.isFocus = !this.isFocus;
      this.$emit(name, e);
    },
    // 输入框change|input事件
    onEvent(name, e) {
      this.$emit(name, e);
    }
  },
  created() {
    const { digit, password, type } = this;
    this.inputType = digit ? "text" : password ? "password" : type; // 设置input的type属性初始值
  },
  mounted() {
    const { setInputPadding } = this;
    setInputPadding(0);
    setInputPadding(1);
  },
  watch: {
    // 监听参数value的变化
    value(value) {
      this.inputVal = value; // 设置value
    },
    // 监听输入框的值的变化
    inputVal(value, oldValue) {
      // 判断是否为整数输入
      if (this.digit && !/^\d*$/g.test(value)) {
        this.inputVal = +oldValue; // 设置value
      }
      this.$emit("input", value);
    },
    // 监听短信验证状态
    smsIs() {
      this.setInputPadding(1); // 设置input的padding
    }
  }
};
</script>