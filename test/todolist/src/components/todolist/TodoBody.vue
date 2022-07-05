<template>
  <!-- 使用按键修饰符,实现添加 -->
  <input
    type="text"
    name=""
    id=""
    v-model="inputValue"
    @keyup.enter="handleClick()"
  >
  <!-- button按钮,创建点击事件,添加 -->
  <button @click="handleClick()">添加</button>
  <li
    v-for="(item, index) in list"
    :key="index"
  >
    {{item}}
  </li>
</template>

<script>
export default {
  data() {
    return {
      list: [1, 2, 3, 4],
      inputValue: "",
    };
  },
  methods: {
    handleClick() {
      if (this.inputValue != "") {
        this.list.push(this.inputValue);
        this.inputValue = "";
      }
    },
  },
};
</script>

<style>
</style>