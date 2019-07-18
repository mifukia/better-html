<template>
  <v-layout>
    <v-flex xs3 class="controller">
      <v-slider v-model="slider" :min="0" :max="100" label="Size" thumb-label></v-slider>
      <input type="file" @change="onFileChange" />
    </v-flex>
    <v-flex xs9 class="main">
      <div class="img" v-show="uploadedImage">
        <img :src="uploadedImage" :style="{width:slider + '%'}" />
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  data() {
    return {
      slider: 56,
      tile: true,
      uploadedImage: "",
      img_name: ""
    };
  },
  computed: {
    avatarSize() {
      return `${this.slider}px`;
    }
  },
  methods: {
    onFileChange(e) {
      const files = e.target.files || e.dataTransfer.files;
      this.createImage(files[0]);
      this.img_name = files[0].name;
    },
    // アップロードした画像を表示
    createImage(file) {
      const reader = new FileReader();
      reader.onload = e => {
        this.uploadedImage = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    remove() {
      this.uploadedImage = false;
    }
  }
};
</script>

<style>
.controller {
  background: rgb(233, 232, 232);
  padding: 10px;
}
.main {
  padding-left: 20px;
  border: 1px solid #eee;
}
</style>

