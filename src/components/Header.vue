<template>
  <div class="header">{{ title }}</div>
</template>

<script>
export default {
  props: {
    titlename: {
      default: "",
      type: String,
    },
  },
  data() {
    return {
      title: this.titlename,
    };
  },
};
</script>

<style>
.header {
  background-color: rgb(65, 65, 243);
  color: white;
  height: 50px;
  line-height: 50px;
  text-align: center;
}
</style>