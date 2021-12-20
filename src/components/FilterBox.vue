<template>
  <div
    :class="filter_kind"
    class="filter-item"
    :style="`background-image:url(${Image})`"
    @click="fire"
  >
    <slot></slot>
  </div>
  <!-- :class="filter_kind + ' filter-item'" -->
</template>

<script>
export default {
  name: "FilterBox",
  methods: {
    fire() {
      this.emitter.emit("Select_Filter", this.filter_kind);
    },
  },
  props: {
    Image: String,
    filter_kind: String,
  },
};
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
  background-position: center;
}
</style>
