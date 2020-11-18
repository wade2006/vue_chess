<template>
  <div>
    <div class="cell" v-on:click="onClickSelf">
      <template v-if="status">{{ text }}</template>
      <template v-else></template>
    </div>
  </div>
</template>

<script>
export default {
  props: ["n", "isfinish"],
  data() {
    return {
      status: false,
      text: null,
    };
  },
  methods: {
    onClickSelf() {
      if (this.isfinish) {
        return;
      }
      if (this.text != null) {
        return;
      }
      this.status =true;
      this.text = this.n % 2 === 0 ? "x" : "o";
      this.$emit("click", this.text);
    },
  },
};
</script>
<style>
.cell {
  border: 1px solid #000;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 80px;
}
</style>
