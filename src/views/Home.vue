<template>
  <v-layout>
    <v-flex xs3 class="controller">
      <v-slider v-model="slider" :min="0" :max="100" label="Size" thumb-label></v-slider>
      <input type="file" @change="onFileChange" />
      <v-select :items="cols" label="Standard"></v-select>
      <v-btn color="primary">ADD</v-btn>
    </v-flex>
    <v-flex xs9 class="main">
      <div class="img" v-show="uploadedImage">
        <img :src="uploadedImage" :style="{width:slider + '%'}" />
      </div>
      <v-layout class="els" wrap>
        <v-flex xs12 class="el" v-for="(element,i) in elements" :key="i">
          <v-layout>
            <v-flex v-for="(child,i) in element.child" :key="i">
              <div class="el">
                <p v-if="child.text">{{child.text}}</p>
              </div>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
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
      img_name: "",
      // elements: [
      //   {
      //     tag: "ul",
      //     col: 1,
      //     child: [
      //       {
      //         tag: "li",
      //         col: "xs4",
      //         text: "ダミーテキスト",
      //         child: null
      //       },
      //       {
      //         tag: "li",
      //         col: "xs4",
      //         text: "ダミーテキスト",
      //         child: null
      //       },
      //       {
      //         tag: "li",
      //         col: "xs4",
      //         text: "ダミーテキスト",
      //         child: null
      //       }
      //     ]
      //   }
      // ],
      elements: [
        {
          tag: "p",
          col: 1,
          child: [
            {
              tag: "li",
              col: "xs4",
              text: "ダミーテキスト",
              child: null
            },
            {
              tag: "li",
              col: "xs4",
              text: "ダミーテキスト",
              child: null
            },
            {
              tag: "li",
              col: "xs4",
              text: "ダミーテキスト",
              child: null
            }
          ]
        },
        {
          tag: "p",
          col: 1,
          child: null
        }
      ],
      cols: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
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

<style lang="scss" scoped>
.controller {
  background: rgb(233, 232, 232);
  padding: 10px;
}
.main {
  padding-left: 20px;
  border: 1px solid #eee;
}
.el {
  border: 1px solid rgb(233, 232, 232);
  height: 150px;
  p {
    margin: 0;
  }
}
</style>

