<template>
  <section class="footer">
    <div class="footer-left">
      <input
        type="checkbox"
        id="allcheck"
        :checked="allchecked"
        @change="notice"
      />
      <label for="allcheck">全选</label>
    </div>
    <div class="footer-middle">￥ {{ totalPrice }}</div>
    <button type="button" class="footer-right">结算</button>
  </section>
</template>

<script>
export default {
  props: {
    allchecked: {
      type: Boolean,
      required: true,
    },
    totalPrice: {
      default: 0,
      type: Number,
    },
  },
  methods: {
    notice(e) {
      this.$emit("changeAll", e.target.checked);
    },
  },
};
</script>

<style lang="less">
@footh: 50px;
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;
  bottom: 0;
  left: 0;
  width: 100%;
  height: @footh;
  background: whitesmoke;
}
.footer-right {
  width: 100px;
  height: 80%;
  border-radius: @footh*0.8 / 2;
  background: skyblue;
  outline: none;
  border-width: 0;
  margin-right: 30px;
  padding: 0;
  font-size: 20px;
}
.footer-left {
  margin-left: 30px;
}
.footer-middle {
  color: red;
}
</style>