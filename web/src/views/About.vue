<template>
  <div class="about">
    <h1 style="width: 200px">各餐廳簡介</h1>
    <div class="card-content-body">
      <div
        class="card-content"
        v-for="(restaurant, index) in restaurants"
        :key="index"
      >
        <img class="card-content-img" :src="restaurant.image" alt="image" />
        <div class="card-content-title">{{ restaurant.name }}</div>
        <div class="card-content-para">
          {{ restaurant.description }}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import gql from "graphql-tag"

export default {
  data() {
    return {
      imageSources: [
        { image: require("../assets/yifong.png"), name: "一風堂拉麵" },
        { image: require("../assets/dahe.png"), name: "大河屋燒肉丼串燒" },
        { image: require("../assets/shito.png"), name: "石頭日式炭火燒肉" },
        { image: require("../assets/diyiming.png"), name: "第一名火烤兩吃" },
        { image: require("../assets/yudoufu.png"), name: "玉豆腐 韓式料理" },
        {
          image: require("../assets/holezhihan.png"),
          name: "虎樂日韓精肉海鮮火烤吃到飽",
        },
        { image: require("../assets/junshoushi.png"), name: "藏壽司" },
        { image: require("../assets/julu.png"), name: "逐鹿炭火燒肉" },
        { image: require("../assets/ertanhogo.png"), name: "貳堂火鍋" },
        { image: require("../assets/shueueshan.png"), name: "雪嶽山韓式料理" },
        { image: require("../assets/dingtaifen.png"), name: "鼎泰豐" },
      ],
    }
  },
  apollo: {
    restaurants: {
      query: gql`
        query {
          restaurants {
            id
            name
            description
          }
        }
      `,
      result({ data }) {
        data.restaurants.forEach((restaurant) => {
          this.imageSources.forEach((source) => {
            source.name === restaurant.name
              ? (restaurant.image = source.image)
              : ""
          })
        })
      },
    },
  },
  methods: {},
}
</script>
<style scoped>
.about {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.card-content-body {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: right;
  padding: 10px 30px;
}
.card-content {
  margin: 10px;
  background: rgb(228, 228, 228);
  height: 350px;
  width: 250px;
  box-shadow: 3px 3px 8px 0 #959595;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
}
.card-content-img {
  border-radius: 10px 10px 0 0;
  box-shadow: 3px 3px 8px 0 #959595;
  max-width: 250px;
  height: 150px;
}
/* .card-content-img:hover {
  max-width: 300px;
} */

img:hover {
  transition: all 0.3s ease 0s;
  transform: scale(1.1, 1.1);
}
.card-content-title {
  padding-top: 10px;
  text-shadow: 1px 1px rgb(139, 139, 139), -1px -1px rgb(231, 204, 204),
    1px -1px rgb(204, 249, 255), -1px 1px rgb(226, 213, 255);
  font-size: 16px;
  background: linear-gradient(rgb(255, 255, 255), rgb(162, 205, 255));
}
.card-content-para {
  background: linear-gradient(rgb(255, 217, 217), rgb(213, 255, 225));
  border-radius: 0 0 10px 10px;
  font-size: 14px;
  line-height: 24px;
  font-weight: bold;
  width: 230px;
  padding: 10px;
  margin-bottom: 4px;
  flex: 1;
  overflow: scroll;
}
</style>
