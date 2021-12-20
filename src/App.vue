<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="Step == 1" @click="Step++">Next</li>
      <li v-if="Step == 2" @click="Publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :Data="Data" :Step="Step" :Image="Image" @write="write = $event" />
  <!-- <button v-if="Step == 0" @click="more">더보기</button> -->

  <div class="footer">
    <ul class="footer-button-plus">
      <input
        @change="upload"
        accept="image/*"
        type="file"
        id="file"
        class="inputfile"
      />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>
import Container from "./components/Container.vue";
import Data from "./assets/content.js";
// import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      Data: Data,
      Count: 0,
      Step: 0,
      Image: "",
      write: "",
      select_filter: "",
    };
  },

  mounted() {
    this.emitter.on("Select_Filter", (result) => {
      this.select_filter = result;
    });
  },

  methods: {
    Publish() {
      var Content = {
        name: "Siheon_9709",
        userImage: require("./assets/images/siheon.jpg"),
        postImage: this.Image,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.write,
        filter: this.select_filter,
      };
      this.Data.unshift(Content);
      this.Step = 0;
      console.log(Content.filter);
    },
    // more() {
    //   axios
    //     .get(`https://codingapple1.github.io/vue/more${this.Count}.json`)
    //     .then((result) => {
    //       console.log(result);
    //       this.Data.push(result.data);
    //       this.Count++;
    //     });
    // },
    upload(e) {
      let file = e.target.files;
      console.log(file);
      let url = URL.createObjectURL(file[0]);
      console.log(url);
      this.Image = url;
      this.Step++;
    },
  },
  components: {
    Container: Container,
  },
};
</script>

<style>
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
</style>
