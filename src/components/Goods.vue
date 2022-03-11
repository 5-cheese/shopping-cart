<template>
  <div class="good-container">
    <div class="good-btn">
      <input
        :id="'good' + id"
        class="btn-choose"
        type="checkbox"
        @change="notice"
        :checked="state"
      />
    </div>
    <label class="good-img" :for="'good' + id"
      ><img :src="pic" alt="加载失败"
    /></label>
    <div class="good-des">
      <div class="des-hd">{{ title }}</div>
      <span class="des-price">￥{{ price }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      required: true,
      type: Number,
    },
    title: {
      default: "标题",
      type: String,
    },
    pic: {
      default: "#",
      type: String,
    },
    price: {
      default: 0,
      type: Number,
    },
    state: {
      default: true,
      type: Boolean,
    },
  },
  methods: {
    notice(e) {
      let newState = e.target.checked;
      this.$emit("state-change", { id: this.id, state: newState });
    },
  },
};
</script>

<style lang="less">
.good-container {
  padding: 10px 0;
  margin: 0;
  overflow: hidden;
  height: 125px;
  border-bottom: 1px solid #7f7f7f;
  img {
    height: 100%;
    width: 100%;
    // vertical-align: middle;
    display: block;
  }
  .good-img {
    :hover {
      cursor: pointer;
    }
    float: left;
    height: 100%;
    width: 110px;
  }
  .good-des {
    position: relative;
    height: 100%;
    width: 50vw;
    float: left;
  }
  .good-btn {
    position: relative;
    float: left;
    height: 100%;
    width: 40px;
    .btn-choose {
      position: absolute;
      top: 50px;
      left: 12px;
    }
  }
}
.des-hd {
  font: normal 700 14px "Times New Roman", Georgia, Serif;
  padding: 5px;
}
.des-price {
  position: absolute;
  //   padding: 2px;
  bottom: 5px;
  left: 5px;
  color: red;
}
</style>