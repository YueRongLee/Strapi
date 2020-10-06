<template>
  <div class="draw-lots-page">
    <h1 style="width: 200px">今天吃哪間</h1>
    <rotate-name :awards="names" />
  </div>
</template>
<script>
import RotateName from "../components/RotateName"
import gql from "graphql-tag"

export default {
  components: {
    "rotate-name": RotateName,
  },
  data() {
    return {
      names: [],
    }
  },
  methods: {},
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
        this.names = []
        for (let i = data.restaurants.length; i > 10; i--) {
          let random = Math.random() * i
          data.restaurants.splice(random, 1)
        }
        data.restaurants.forEach((r) => {
          this.names.push(r.name)
        })
      },
    },
  },
}
</script>
<style scoped>
.draw-lots-page {
  display: flex;
  height: 100%;
  flex-direction: column;
}
</style>
