<template>
  <div class="scroll-wrap" @touchmove.stop="touchmove">
    <div class="home">
      <input
        ref="actual-input"
        class="actual-input"
        :style="actualInputStyle"
        type="text"
        v-model="value"
        placeholder="请输入"
        @focus="actualInputFocus"
        @blur="actualInputBlur"
      />
      <div
        ref="virtual-input"
        class="virtual-input"
        :style="virtualInputStyle"
        @click="virtualInputClick"
      >
        {{ value || "请输入" }}
      </div>

      <ul style="padding: 0; margin: 0">
        <li>value = {{ value }}</li>
        <li>originalHeight = {{ originalHeight }}</li>
        <li>focusHeight = {{ focusHeight }}</li>
        <li>keyboreHeight = {{ keyboreHeight }}</li>
        <li v-for="i in 100" :key="i">{{ i }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      value: "",
      criticalTime: 400, // 键盘抬起时可以监听到visualViewport.height变化的临界值
      originalHeight: "",
      focusHeight: "",
      actualInputStyle: {},
      virtualInputStyle: {},
    };
  },
  computed: {
    keyboreHeight() {
      return this.originalHeight - this.focusHeight;
    },
  },
  created() {
    this.originalHeight = visualViewport.height;
    this.actualInputStyle = {
      transform: "translateY(0)",
      opacity: 0,
    };
    this.virtualInputStyle = {
      transform: "translateY(" + visualViewport.height + "px)",
      opacity: 1,
    };
  },
  methods: {
    touchmove() {
      this.$refs["actual-input"].blur();
    },
    virtualInputClick() {
      this.$refs["actual-input"].focus();
    },
    actualInputFocus() {
      setTimeout(() => {
        this.focusHeight = visualViewport.height;
        this.actualInputStyle = {
          transform: "translateY(" + visualViewport.height + "px)",
          opacity: 1,
        };
        this.virtualInputStyle = {
          transform: "translateY(0)",
          opacity: 0,
        };
      }, this.criticalTime);
    },
    actualInputBlur() {
      this.actualInputStyle = {
        transform: "translateY(0)",
        opacity: 0,
      };
      this.virtualInputStyle = {
        transform: "translateY(" + this.originalHeight + "px)",
        opacity: 1,
      };
    },
  },
};
</script>

<style lang="less" scoped>
.home {
  padding: 100px 20px;
  .actual-input,
  .virtual-input {
    box-sizing: border-box;
    background-color: #ffffff;
    padding: 10px;
    margin: 0;
    font-size: 16px;
    width: 100%;
    height: 50px;
    line-height: 28px;
    outline: none;
    border: none;
    border-top: 1px solid #cccccc;
    border-radius: 0;
    position: fixed;
    top: -50px;
    left: 0;
    right: 0;
  }
}
</style>
