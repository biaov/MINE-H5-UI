<template>
  <!-- 复选框 -->
  <div class="me-checkbox" @click="handleClick" :aria-checked="isChecked+''" :aria-disabled="disabled+''">
    <me-icon :name="iconName" :color="isChecked?checkedColor:''" :size="iconSize"></me-icon>
    <div class="u-value">
      <slot></slot>
    </div>
  </div>
</template>
<script>
import MeIcon from "~/MeIcon";
export default {
  name: "MeCheckbox",
  components: {
    MeIcon
  },
  props: {
    // v-model的值
    value: {
      type: Boolean,
      default: false
    },
    // 单选框索引名称
    name: {
      type: [String, Number]
    },
    // 图标形状
    shape: {
      type: String,
      default: "round" // square|round
    },
    // 自定义图标
    icon: {
      type: String,
      default: ""
    },
    // 自定义选中图标
    iconSelect: {
      type: String,
      default: ""
    },
    // 图标大小
    iconSize: {
      type: String,
      default: "20px"
    },
    // 选中状态颜色
    checkedColor: {
      type: String,
      default: ""
    },
    // 禁用状态
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isChecked: this.value, // 是否选中
      iconName: "" // 图标名称
    };
  },
  methods: {
    // 点击单选框
    handleClick() {
      const {
        isChecked,
        name,
        setIcon,
        disabled,
        $parent: { $options, onChange }
      } = this;
      // 判断当前是否被禁用
      if (!disabled) {
        // 判断是否存在父组件
        if ($options._componentTag === "me-checkbox-group") {
          onChange({ name, isChecked });
        } else {
          this.isChecked = !isChecked; // 改变当前状态
          this.$emit("input", !isChecked);
        }
        this.$emit("on-click");
        setIcon();
      }
    },
    // 设置图标
    setIcon() {
      const { icon, iconSelect, isChecked, shape } = this;
      this.iconName = isChecked
        ? iconSelect
          ? iconSelect
          : shape === "round"
          ? "icon-radio"
          : "icon-baseline-check_box-px"
        : icon
        ? icon
        : shape === "round"
        ? "icon-radio3"
        : "icon-baseline-check_box_outline_blank-px";
    },
    // 设置状态
    setStatus() {
      const {
        value,
        name,
        setIcon,
        $parent: { $options, currentValue }
      } = this;
      this.isChecked = $options._componentTag === "me-checkbox-group" ? currentValue.includes(name) : value;
      setIcon();
    }
  },
  created() {
    this.setStatus();
  },
  watch: {
    // 监听数据绑定
    value(value) {
      this.isChecked = value;
      this.setIcon();
    }
  }
};
</script>