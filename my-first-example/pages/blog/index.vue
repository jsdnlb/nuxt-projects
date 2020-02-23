<template>
  <div class="container mt-5">
    <div class="card my-2" v-for="(item, index) in items" :key="index">
      <div class="card-body">
        <nuxt-link :to="`blog/${item.id}`">
          <h1>{{ item.title }}</h1>
        </nuxt-link>
        <p>
          {{ item.body }}
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      items: []
    };
  },
  async created() {
    try {
      const res = await axios.get(
        "https://jsonplaceholder.typicode.com/posts?_limit=10"
      );
      // console.log("TCL: created -> res", res.data);
      this.items = res.data;
    } catch (error) {
      console.log("TCL: created -> error", error);
    }
  },
  head: {
    title: "Esta es mi página de inicio",
    meta: [
      {
        hid: "description",
        name: "description",
        content: "Esta es la descripción de mi página de inicio"
      }
    ]
  }
};
</script>
