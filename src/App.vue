<template>
  <div id="app">
    <Header :titlename="'购物车'"></Header>
    <Goods
      @state-change="getChange"
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :pic="item.goods_img"
      :title="item.goods_name"
      :price="item.goods_price"
      :state="item.goods_state"
    ></Goods>
    <Footer
      :allchecked="allchecked"
      :totalPrice="totalPrice"
      @changeAll="dealAS"
    ></Footer>
  </div>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header.vue";
import Goods from "@/components/Goods.vue";
import Footer from "@/components/Footer.vue";
export default {
  components: {
    Header,
    Goods,
    Footer,
  },
  data() {
    return {
      list: [],
    };
  },
  computed: {
    allchecked() {
      return this.list.every((item) => item.goods_state);
    },
    totalPrice() {
      let t = 0,
        list = this.list;
      for (let i = 0; i < list.length; i++)
        if (list[i].goods_state) t += list[i].goods_price;
      return t;
    },
  },
  methods: {
    async initCartList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      console.log(res);
      if (res.status === 200) this.list = res.list;
    },
    getChange(val) {
      let { id, state: newState } = val;
      console.log(id + ": " + newState);
      this.list.some((item) => {
        if (item.id === id) {
          item.goods_state = newState;
          return true;
        }
      });
    },
    dealAS(val) {
      this.list.forEach((item) => (item.goods_state = val));
    },
  },
  created() {
    this.initCartList();
  },
};
</script>

<style lang="less">
#app {
  margin-top: 30px;
  padding: 0 10px;
}
</style>
