<template>
  <div class="about">
    <h1>抽抽樂</h1>
    <rotate-name :awards="names" />
    <!-- <rotate-result /> -->
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
.about {
  display: flex;
  height: 100%;
  flex-direction: column;
  align-items: center;
}
</style>
