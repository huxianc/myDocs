- 统一 dialog 后面更改会方便一些

```html
<template>
  <el-dialog
    :visible.sync="visibleDialog"
    v-bind="$attrs"
    v-on="$listeners"
    :width="width"
    center
  >
    <slot></slot>
    <template #footer>
      <el-button type="primary" @click="$_handleConfirm"
        >{{ confirmButtonText }}</el-button
      >
      <el-button @click="$_handleCancel">取 消</el-button>
    </template>
  </el-dialog>
</template>
```

```js
<script>
export default {
  name: "HXDialog",
  inheritAttrs: false,
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
    confirmButtonText: {
      type: String,
      default: "确 定",
    },
    width: {
      type: String,
      default: "400px",
    },
  },
  computed: {
    visibleDialog: {
      get() {
        return this.visible;
      },
      set(val) {
        this.$emit("update:visible", val);
      },
    },
  },
  methods: {
    $_handleCancel() {
      this.$emit("cancel");
    },
    $_handleConfirm() {
      this.$emit("confirm");
    },
  },
};
</script>
```
