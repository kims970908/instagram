<template>
  <div>
    <div v-if="Step == 0">
      <Post
        :Data="Data[Count]"
        v-for="(Content_data, Count) in Data"
        :key="Count"
      />
    </div>
    <!-- 필터선택페이지 -->
    <div v-if="Step == 1">
      <div
        :class="select_filter"
        class="upload-image"
        :style="{ backgroundImage: `url(${Image})` }"
      ></div>
      <div class="filters">
        <FilterBox
          v-for="filter_kind in filter"
          :key="filter_kind"
          :Image="Image"
          :filter_kind="filter_kind"
          ><span>{{ filter_kind }}</span>
        </FilterBox>
      </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="Step == 2">
      <div
        :class="select_filter"
        class="upload-image"
        :style="{ backgroundImage: `url(${Image})` }"
      ></div>
      <div class="write">
        <textarea
          @input="$emit('write', $event.target.value)"
          class="write-box"
          placeholder="write!"
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "./Post.vue";
import FilterBox from "./FilterBox.vue";
import filter from "../assets/filter.js";
export default {
  name: "Container",
  data() {
    return {
      filter: filter,
      select_filter: "",
    };
  },
  mounted() {
    this.emitter.on("Select_Filter", (result) => {
      this.select_filter = result;
    });
  },
  props: {
    Data: Array,
    Step: Number,
    Image: String,
  },
  components: {
    Post: Post,
    FilterBox: FilterBox,
  },
};
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>
